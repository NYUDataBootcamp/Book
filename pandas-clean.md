# Pandas 2: Cleaning data

---
**Overview.**  The dirty secret of data work is that data almost never comes in the form we want.  Here we run through a variety of methods for taking messy data and turning it into clean, nicely formatted data.

**Python tools.** Changing variable values and types, selecting variables and observations, transposing and pivoting data.

**Buzzwords.**  Selection, filtering, pivoting; **want operator**.

**Applications.** Entry poll, Chipotle, World Economic Outlook.

**Code.** Link.

---

**UNDER CONSTRUCTION**

Data rarely never comes in the form we want.  There are more problems than we can count, but here are a few we've run across:

* Numerical entries are contaminated by commas (thousands) and dollar signs, leading Pandas to interpret them as strings.
* The row or column labels are contaminated.  In one example, country names included numbers, indicating footnotes in the source spreadsheet:  `Canada 1`, `Chile 2`, and so on.
* Missing values are marked in erratic ways.  The most treacherous example we've seen marked an elipsis:  ...  You might think we could represent that by the string `'...'`, but in fact it was a single character, a unicode elipsis.  How did we figure that out?  We used the `len()` function and found it had length one.
* We want to select certain variables or observations from a larger set.
* Variables run across rows, rather than down columns.
* Columns and rows are mixed up in some way other than how we want them.

We'll surely see more than this as we proceed, but that gives us a good start.

We describe solutions to the first four issues as data **cleaning**.  The next one as **selection**.  And the last two as **shaping**.  We address them in turn, using examples from datasets we use ourselves.



## Reminders

* Pandas.  Python's data package.

* Dataframes.  A dataframe `df` is a data structure that includes a table of data, similar to a spreadsheet, plus row labels (`df.index`) and column labels (`df.columns`).  Typically columns are variables and rows are observations.

* Dataframe methods.  Some of our favs are `shape`, `head` and `tail`, `dtypes`, `rename`, `drop`, `set_index`, `T` (transpose), and `plot`.  Remind yourself what they do -- or look them up.

* Series.  A series is a single variable, such as a column of a dataframe:  `df['variable']`.  Similar to a dataframe, but the available methods differ a little.

<!--
Some of these are attributes
-->

* List comprehensions.  A clever feature of Python that lets us do implicit loops over lists.  It's particularly useful for refining variable names.  Example:  If the list of variable names is `names = ['variable1', 'variable2']`, we can capitalize them with the list comprehension

   ```python
   [name.title() for name in names]
   ```

   (The `title` method takes a string and capitalizes the first letter -- what's called "title case.")


**Exercise.** Consider the dataframe defined by

```python
import pandas as pd
data = {'EG.ELC.ACCS.ZS': [53.2, 47.3, 85.4, 22.1],    # access to elec (%)
        'IT.CEL.SETS.P2': [153.8, 95.0, 130.6, 74.8],  # cell contracts per 100
        'IT.NET.USER.P2': [11.5, 12.9, 41.0, 13.5],    # internet access (%)
        'Country': ['Botswana', 'Namibia', 'South Africa', 'Zambia']}
af = pd.DataFrame(data)
```

* What are its dimensions?
* What are its dtypes?  What does this mean?
* Set the index to `'Country'`.
* Change the name of the first variable to `'elect'`.
* Use the `plot` method to produce a bar chart of the whole dafaframe.  What does it use as its x axis?


<!--
```python
data = {'countrycode': ['CHN', 'CHN', 'CHN', 'FRA', 'FRA', 'FRA'],
        'pop': [1124.8, 1246.8, 1318.2, 58.2, 60.8, 64.7],
        'rgdpe': [2.611, 4.951, 11.106, 1.294, 1.753, 2.032],
        'year': [1990, 2000, 2010, 1990, 2000, 2010]}
pwt = pd.DataFrame(data)
```
-->

One more reminder:  Download the code file for this chapter and save it in your `Data_Bootcamp` directory.


## The "want operator"

When we're writing code, it's essential that we keep our goals -- our "wants" -- in mind.  In the words of a colleague, we need to apply the **want operator**.  By which we mean:  Start with what we want, then figure out how to get there.

Here are some examples of data that comes in a form that's not as useful as it might be.

**Chipotle.**  The [New York Times](http://www.nytimes.com/interactive/2015/02/17/upshot/what-do-people-actually-order-at-chipotle.html) wrote an article about the number of calories in a typical Chipotle order.  Even better, they posted their data on the web.   In their data, every row describes the purchase of a specific item:  the item, the quantity, the price, and so on.  Orders typically consists of multiple items.

Let's say our goal is to compute the price of a typical order. [Daniel Forsyth](http://www.danielforsyth.me/pandas-burritos-analyzing-chipotle-order-data-2/) noted that the prices of individual items are entered with dollar signs, which means Python reads them as strings and assigns the price variable the dtype object.

(Take a breath and remind yourself what this means.  Ok, ready?)

Here's some code to illustrate the point:

```python
url = 'https://raw.githubusercontent.com/TheUpshot/chipotle/master/orders.tsv'
chp = pd.read_csv(url, sep='\t')   # tab (\t) delimited
print('Variable dtypes:\n', chp.dtypes, sep='')
print(chp.head())
```

The first print statement gives us

```python
Variable dtypes:
order_id               int64
quantity               int64
item_name             object
choice_description    object
item_price            object
dtype: object
```

This tells us, among other things, that the variable `item_price` has dtype object.  That means, specifically, that it's not a number.  The second print statement lists the first five entries, where we see the culprit:  the dollar signs ($).  Our want is to eliminate the dollar sign and convert the variable to a float, which we can then use to calculate the price of an order.

**Entry poll.**  We collected your responses to a short poll at the start of the term.  Google records the answers in a spreadsheet.  Each column is a question and each row is a responder (anonymous).  So far so good.  But the column labels consist of the whole question, so they're a bit unwieldy.  And the responses consist of the whole response, which is also a bit unwieldy.

What, then, are our wants?  We want to trim both the column labels and the responses.

Here we see it in action:

```python
import pandas as pd
url1 = 'http://pages.stern.nyu.edu/~dbackus/Data/'
url2 = 'Data-Bootcamp-entry-poll_s16.csv'
url = url1 + url2
ep = pd.read_csv(url, header=0)
print('Dimensions:', ep.shape)
print('\nData types:\n', ep.dtypes, sep='')
```



**OECD healthcare stats.** The goal here is to produce a bar chart for a recent year of the number of doctors (per thousand population) for a selection of countries.  We read in the data with

```python
url1 = 'http://www.oecd.org/health/health-systems/'
url2 = 'OECD-Health-Statistics-2015-Frequently-Requested-Data.xls'
docs = pd.read_excel(url1+url2,
                     skiprows=3,
                     sheetname='Physicians',
                     index_col=0,
                     skip_footer=21)
print('Dimensions:', docs.shape)
print('Variable dtypes:\n', docs.dtypes, sep='')
print(docs.head())
```

Here we have a number of problems that we want to correct:

* The data consists of numbers (number of doctors per thousand people) but the dtype is mostly object.  We can't plot that, we need numbers.
* We want to choose data for a specific recent date (2013?) and a subset of countries (Canada, France, Germany, Japan, the UK, and the US).
* The index (country name) includes an integer that comes from a footnote in the file.  The plot method will use the index to label the graph and we'd prefer not to have footnotes messing it up.


**World Economic Outlook.**  This is the IMF's semiannual international dataset of macroeconomic variables.  Our goal here is to plot government debt (expressed as a percentage of GDP) over time for a selection of countries (Argentina, Germany, Greece, and the United States).  This code reads in the data:

```python
url1 = 'http://www.imf.org/external/pubs/ft/weo/2015/01/weodata/'
url2 = 'WEOApr2015all.xls'
url = url1 + url2
weo = pd.read_csv(url, sep='\t') #, thousands=',', na_values=['n/a', '--'])
```

There's a lot here, so we carve out some pieces and print them:

```python
small = weo[list(weo[list(range(12))])]     # grab first 12 columns
print('Variable dtypes:\n', small.dtypes, sep='')
print('\nFirst 9 variables:\n', small[list(range(9))].head(), sep='')
print('\nNext 3 variables (data):\n', small[list(range(9,12))].head(), sep='')
```

We see that the first nine variables are descriptions:  country, country code, variable, variable code, variable description, units, and so on.  The next three are the start of the data, which continues to 2015 and beyond.  A close examination reveals some problems:

* Missing values need to be identified.
* Large numbers have commas in them that lead Pandas to give variables the dtype object.  (This is true, but it takes some effort to find examples.)

Both can be handled in the read statement by deleting the hash in the read statement, so that's what we'll do.  But there's another one that's not so easy:

* Variables run across rows, rather than down columns.  We see this in the column labels:  '1980', '1981', etc.  (And yes, dates are treated as strings here.  Try `weo['1980']`.) The plot method assumes observations run down columns, so we'll have to switch the rows and columns.


## String methods

Here the issue is that we tring data that we want to change in some way.

startswith()
extract()



## Selection

Suppose we want to choose some variables or observations, but not others.  That's referred to variously as selection, subsetting, slicing, and filtering.  We'll use the term **selection* since it seems to mean what it sounds like.  We'll ignore selection based on row and column labels or numbers, which we don't use all that much.

**Selecting a list of variables.**

isin





## Cleaning data

* Kill $'s
* Kill commas in numbers
* astype
* Strip off excess in indexes (OECD healthcare)

astype



## Renaming indexes

Apply list comprehension to OECD doc data...





## Switching rows and columns

transpose

pivot





<!--
## Missing values

nan = float?
-->


<!--
## Dates

How they work, resampling...

http://chrisalbon.com/python/pandas_resample_by_time.html
-->

## Multi-indexes



## Stacking and unstacking


## Melt


## References


<!--

Brandon Rhodes.  This is great.
https://youtu.be/5JnMutdy6Fw
https://github.com/brandon-rhodes/pycon-pandas-tutorial/

https://en.wikipedia.org/wiki/Pivot_table

Other

* Groupby:  http://pandas.pydata.org/pandas-docs/stable/groupby.html
* stack and unstack:  http://pandas.pydata.org/pandas-docs/stable/reshaping.html

Kaggle example:  http://blog.kaggle.com/2013/01/17/getting-started-with-pandas-predicting-sat-scores-for-new-york-city-schools/

Lots of examples:
http://tomaugspurger.github.io/
http://nbviewer.ipython.org/github/TomAugspurger/PyDataSeattle/tree/master/notebooks/

SQL intro https://www.khanacademy.org/computing/hour-of-code/hour-of-sql/v/welcome-to-sql

https://www.reddit.com/r/Python/comments/3wa22v/120gb_csv_is_this_something_i_can_handle_in_python/


SQL and Pandas:  https://www.youtube.com/watch?v=1uVWjdAbgBg

http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/
http://www.gregreda.com/2013/10/26/working-with-pandas-dataframes/

http://manishamde.github.io/blog/2013/03/07/pandas-and-python-top-10/

http://markthegraph.blogspot.com/2014/01/pandas-dataframe-cheat-sheet-and-python.html

http://nicolas.kruchten.com/content/2015/09/jupyter_pivottablejs/

-->