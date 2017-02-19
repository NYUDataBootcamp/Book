# Pandas 1: Introduction

---
**Overview.**  We introduce the Python package pandas and its core type the DataFrame. pandas is the Python package devoted to data management. In this chapter, we cover how to create a DataFrame and discuss some of its properties and methods.

**Python tools.**  pandas, DataFrame, Series

**Buzzwords.**  DataFrame, Series

**Applications.** US GDP

**Code.**  [Link](https://raw.githubusercontent.com/NYUDataBootcamp/Materials/master/Code/Python/bootcamp_pandas-intro.py).

---

The goal of this lecture is to introduce you to some of the basic concepts needed to understand how to do data analysis in Python. In particular, we introduce you to the pandas package and discuss its two core types DataFrames and Series.

It is worth noting that the pandas package could be considered more **[high-level](https://en.wikipedia.org/wiki/High-level_programming_language)** than core Python in the sense of taking a lot of the programming details out of our hands. That makes it easier to use -- lots of things are automated -- but in some cases also a bit more mysterious. All together, though, it's an incredibly powerful collection of data tools which will make your life throughout this class (and beyond) much easier.

## Reminders

* Objects and methods.  Recall that we apply the method `justdoit` to the object `x` with `x.justdoit()`.

* Help.  We get help in Spyder from both the IPython console and the Object inspector.  For the hypothetical `x.justdoit`, we would type `x.justdoit?` in the IPython console or `x.justdoit` in the Object inspector.

* Data structures.  That's the term we use for specific organizations of data.  Examples are lists, tuples, and dictionaries. Each has a specific structure and a set of methods we can apply.  List are (ordered) collections of objects between square brackets:  `numberlist = [1, -5, 2]`.  Dictionaries are (unordered) pairs of items between curly brackets:  `namedict = {'Dave': 'Backus', 'Chase': 'Coleman'}`. The first item in each pair is the "key," the second is the "value.""

* Integers, floats, and strings.  Three common types of data.

* Function returns.  We refer to the output of a function as its **return**.  We would say, for example, that the function `type(x)` `return`s the type of the input object `x`.  We capture the return with an assignment:  `xtype = type(x)`.

* Packages. Packages are collections of tools -- functions and types/methods -- that extend Python's capabilities. We import a package using an `import` (e.g. `import pandas`) statement or some combination of `import`, `from`, and `as` (e.g. `import pandas as pd` or `from pandas import DataFrame`).

## First Look at DataFrames

The entire pandas package is oriented around the idea of a DataFrame, so it is natural to begin our description of the package there. A DataFrame is similar to a sheet of data in excel (or to an R `data.frame` if you have programmed in R before). Let's create one so that we can see what it looks like (don't forget to run `import pandas as pd` first -- all of our examples will be based on you having previously done this). Let's create our first DataFrame by using data from a dictionary.

```python
# This dictionary is similar to one that we saw earlier in the class
# It represents GDP/CPI data at 10 year intervals from 1990 to 2010
df = pd.DataFrame({"GDP": [5974.7, 10031.0, 14681.1],
                   "CPI": [127.5, 169.3, 217.488],
                   "Year": [1990, 2000, 2010],
                   "Country": ["US", "US", "US"]})
print(df)
```

What do you see on your screen? The print command on our DataFrame should have displayed something that looks like this:

```
       CPI Country      GDP  Year
0  127.500      US   5974.7  1990
1  169.300      US  10031.0  2000
2  217.488      US  14681.1  2010
```

We can verify that this type is indeed a DataFrame (and that we haven't been lying to you about what you created) by simply asking Python to tell us its type:

```python
type(df)
```

returns

```
pandas.core.frame.DataFrame
```

The text prior to DataFrame just tells us some things about where this type lives within pandas -- You can safely ignore it. Now we should talk about what makes up a DataFrame.

* At the top of each of the columns of the dataframe, you should see "CPI", "Country", "GDP", and "Year" (which were the keys to our dictionary). These are known as the _column labels_ or _column names_.
* To the left of the columns, we see a 0, 1, and 2. These numbers are elements of the _index_ (or _row labels_).
* Finally, inside the _index_ and _column labels_, you should see some data (which corresponds to the values of our dictionary). These are known as the _values_. We refer to the data going down a column as a _column_ and the data going across a row as a _row_.

Typically columns are variables and the column labels give us their names.  In our example, the second column has the name `Year` and its values follow below it.  The rows are then observations, and the row labels give us their names.  This is a standard setup and we'll do our best to conform to it.  If the data come in some other form, we'll try to convert it.

We can get all of the relevant information from our DataFrame by accessing the following properties:

**Dimensions.** We access a DataFrame's dimensions -- the numbers of rows and columns -- using `df.shape`.  Here the answer is `(3, 4)`, so we have 3 rows (observations) and 4 columns (variables).

**Columns and indexes.**  We access the column and row labels directly.  For the DataFrame `df` we read in earlier, we extract column labels with the `columns` method:  `df.columns`.  That gives us the verbose output `Index(['CPI', 'Country', 'GDP', 'Year'], dtype='object')`.  If we prefer to have them as a list, we can use a `tolist` method `df.columns.tolist()`.  That gives us the column names as a list:  `['CPI', 'Country', 'GDP', 'Year']`.

The row labels are referred to as the **index**.  We extract them by accessing `df.index`.  That gives us the verbose output `RangeIndex(start=0, stop=3, step=1)`.  We can convert it to a list by using the same `tolist` method, `df.index.tolist()`, which gives us `[0, 1, 2]`.  In this case, the index is not part of the original data; Pandas inserted a counter for us.  As usual in Python, the counter starts at zero.

**Column data types.**  Pandas allows every column (typically a variable) to have a different data type, but the type must be the same within a column.  With our DataFrame `df`, we get the types by using `df.dtypes`:

```
CPI        float64
Country     object
GDP        float64
Year         int64
dtype: object
```

Evidently `Year` is an  integer and both `CPI` and `GDP` are floats.  They're no different from the types of numbers we came across in the previous chapter.  The column, `Country`, is different though. pandas labeled this one as having type `object`. Object is the name Pandas gives to things it can't turn into numbers -- in our case, strings.  Sometimes, as here, that makes sense: country names like `US` are naturally strings.  But in many cases we've run across, numbers are given the dtype object because there was something in the data that didn't look like a number.  We'll see more of that later on.

**Transpose columns and rows.** If we want to rotate the DataFrame, exchanging columns and rows, we use the `transpose` method:  `df.transpose()` or (more succinctly) `df.T`.  Let's do that with the DataFrame `df` we read in earlier:

```python
dft = df.T
print('\n', dft)
```

The result is

```
CPI       127.5  169.3  217.488
Country      US     US       US
GDP      5974.7  10031  14681.1
Year       1990   2000     2010
```

It doesn't make much sense in this case, but in others we'll find it helpful.

**Exercise.** Let's apply what we have learned to the DataFrame generated by this code:

```python
data = {'countrycode': ['CHN', 'CHN', 'CHN', 'FRA', 'FRA', 'FRA'],
        'pop': [1124.8, 1246.8, 1318.2, 58.2, 60.8, 64.7],
        'rgdpe': [2.611, 4.951, 11.106, 1.294, 1.753, 2.032],
        'year': [1990, 2000, 2010, 1990, 2000, 2010]}
pwt = pd.DataFrame(data)
```

* What kind of object is `data`?
* What are the dimensions of `pwt`?
* What dtypes are the variables?  What do they mean?
* What does `pwt.columns.tolist()` do?  How does it compare to `list(pwt)`?
* *Challenging.* What is `list(pwt)[0]`? Why? What type is it?
* *Challenging.* What would you say is the natural index?  How would you set it?

## Operating on DataFrames

So we have a DataFrame `df` whose columns are variables. One of the great things about pandas is that we can do things with every observation of a variable in one statement.

**Variables = Series.**  In the DataFrame `df` we created earlier, if we wanted to refer to only one of the columns (variables), for example `GDP`, we write `df["GDP"]`.

```python
print(df["GDP"])
```

If we ask what type this is, with

```python
print(type(df['GDP']))
```

We find that it's a `pandas.core.series.Series` -- Similar to as with DataFrames, we refer to this as **series** for short.  A series is essentially a DataFrame with a single variable or column. Anytime we ask for a single variable back, pandas will return us a Series, but if we ask for multiple rows (`df[["GDP", "CPI"]]`) then pandas will return us a DataFrame.

Series are useful because we can do addition, subtraction, division, and multiplication with them. Here are some examples

```python
print(df["GDP"] + df["GDP"])
print(df["GDP"] - df["GDP"])
print(df["GDP"] / df["CPI"])
print(df["CPI"] * df["CPI"])
```

How do you think these operations are happening? How does Python know which two elements to add together etc?

Additionally, we can do operations on a Series with integers or floats. For example

```python
print(df["GDP"] / 10000)
```

**Construct new variables from old ones.** Now that we know how to refer to a variable and about some of the operations we can do between variables, we can construct others from them. We construct two as an example

```python
df['RGDP'] = df['GDP']/df['CPI']
df['GDP_div_1000'] = df['GDP'] / 1000
```

The first line computes the new variable `RGDP` as the ratio of `GDP` to `CPI` (here it does division element by element).  The second computes `GDP_div_1000` as `GDP` divided by `1000` (here it divides everything by 1000).

These statements do two things: they perform the calculation on the right, and they assign it to the variable on the left.  The second step adds the new variables to the DataFrame.  The statement `print('\n', df)` now gives us

```
       CPI Country      GDP  Year       RGDP  GDP_div_1000
0  127.500      US   5974.7  1990  46.860392        5.9747
1  169.300      US  10031.0  2000  59.249852       10.0310
2  217.488      US  14681.1  2010  67.503035       14.6811
```

If we step back for a minute, we might compare this to Excel. If `GDP` and `CPI` are columns, then we might start a new column labeled `RGDP`. We would then compute the value of `RGDP` for the first observation and copy the formula to all of the other observations in that column. Here one line of code computes them all.

**Digression.** There are two syntax issues we should mention.  One is that others -- not us! -- commonly refer to a variable `df[`GDP`]` by `df.GDP`.  That usually works, but not always.  For example, it doesn't work if the variable name contains spaces or conflicts with an existing method.  And we can't assign to it, as we did when we defined `RGDP` above.  The second issue is integer variable names.  We avoid these, too, but if we somehow end up with a variable with an integer label -- `2011`, for example -- we would refer to it by that label: `df[2011]` without quotes.  If you're not sure what type the variable labels are, print `df.columns` and see whether they have quotes.

**Rename variables.**  If we want to change *all the names*, we can assign a list of new names to the DataFrame's column labels. WARNING -- You should be very careful when you do this because unless you're sure of what you're doing then you might rename a variable incorrectly!

```python
df.columns = ["cpi", "country", "gdp", "year", "rgdp", "gdp_div_1000"]
```

Here we've simply changed the column names to lower case.  There's a clever way to do this with a list comprehension:

```python
df.columns = [var.lower() for var in df.columns]
```

The flexibility of string methods and list comprehensions opens up a lot of other possibilities as well. We can also assign new names individually.  Suppose we want to give `gdp` a more informative name such as `ngdp` (which stands for nominal gdp).  We can do that with the statement

```python
df = df.rename(columns={'gdp': 'ngdp'})
```

Note the use of a dictionary that associates the old name (the "key" `gdp`) with the new name (the "value" `ngdp`).  If we want to change more than one variable name, we simply add more items to the dictionary. Additionally, it is worth noting that we needed to assign the return of the `rename` function to `df` again -- This is because most of the pandas functions are making copies of our dataframes. You will have to assign the output of a method to a dataframe frequently.

**Extract variables.**  We just saw that commands like `df['ngdp']` "extract" the variable/series `ngdp` from the DataFrame `df`. In other cases, we may want to extract a set of variables and create a smaller DataFrame.  This happens a lot when our data has more variables than we need.

We can extract variables by name or number.  If by name, we simply put the variable names in a list. If by number, we count (as usual) starting with zero. This code gives us two ways to extract `ngdp` and `rgdp` from `df`:

```python
namelist = ['ngdp', 'rgdp']
numlist  = [2, 4]
df_v1 = df[namelist]
df_v2 = df[numlist]
```

You might verify that the two new DataFrames are identical -- with a small dataframe like this, you can do this by hand by just printing them both out.

Closely related is the `drop` method.  If we want to drop the variable `cpi`, we would use

```python
df.drop(['cpi'], axis=1)
```

Here `axis=1` refers to columns; `axis=0` refers to rows.

**Exercise.**  For the DataFrame `df`, create a variable `diff` equal to the difference of `ngdp` and `rgdp`.  Verify that `diff` is now in `df`.

**Exercise.** How would you extract the variables `ngdp` and `year`?

**Exercise.** How would you drop the variable `diff`? If you print your dataframe again, is it gone? If not, why do you think it is still there?

**Exercise (very challenging).** Use a list comprehension to change the variable names from `['ngdp', 'rgdp', 'gdp_div_1000']` to `['nGDP', 'rGDP', 'GDP_div_1000']`.  *Hint:*  What does `s.replace('gdp', 'GDP')` do to the string `s = "this_is_gdp"`?


## DataFrame methods

One of the great things about DataFrames is that they have lots of methods ready to go.  We'll survey some of the most useful ones at high speed and come back to them when we have more interesting data.

**Data output.** To save a DataFrame to a local file on our computer we use the `df.to_*` family of methods. For example, the methods `df.to_csv()` and `df.to_excel()` produce csv and Excel files, respectively.  Both require a file name as input.  We'll hold off on them until we've addressed files on our computer.

**Clipboard methods.**  We can read from the clipboard and write to it.  Suppose we open a spreadsheet and copy a section of it into the clipboard.  We can paste it into a DataFrame with the statement

```python
df_clip = pd.read_clipboard()
```

Going the other way, we can copy the DataFrame `df` to the clipboard with `df.to_clipboard()`.  From the clipboard, we can paste it into Excel or other applications.  We're not fans of this -- it makes replication hard if we need to do this again -- but it's awful convenient.  We heard about it from one of our former students.

**The top and bottom of a DataFrame.** We commonly work with much larger DataFrames in which it's unwieldy, and perhaps impossible, to print the whole thing.  So we often look at either the top or bottom:  the first few few or last few observations.  The statement `df.head(n)` extracts the top `n` observations and `df.tail()` (with no input) extracts the bottom 5.  This creates a new DataFrame, as we see here:

```python
h = df.head(2)
print(type(h))
print(h)
```

The second print statement gives us the first 2 observations, which is what we requested.

`df.tail(2)` does the same for the bottom of the DataFrame `df`:  the last 2 observations (rows).

**Setting the index.**  We're not stuck with the index in our DataFrame, we can make it whatever we want.  If we want to use `year` as the index, associating observations with the `year` variable, we use the `set_index()` method:

```python
df = df.set_index(['year'])
```

That gives us

```python
          cpi country     ngdp       rgdp  gdp_div_1000
year
1990  127.500      US   5974.7  46.860392        5.9747
2000  169.300      US  10031.0  59.249852       10.0310
2010  217.488      US  14681.1  67.503035       14.6811
```

with `year` now used as the index.

We did something else here that's important: We assigned the result back to `df`. That keeps what we've done in the DataFrame `df`.  If we hadn't done this, `df` would remain unchanged with a counter as its index and our effort to set the index would be lost.

We can reverse what we did here with the `reset_index()` method:

```python
df_reset = df.reset_index()
```

Try it and see.  We'll spend more time on these methods in a couple weeks.

**Statistics.**  We can compute the mean, the standard deviation, and other statistics for all the variables (this means that they are operating column by column) at once with

```python
df.mean()
df.std()
df.describe()
```

The first line gives us the means, the second the standard deviations.  The third line gives us a collection of statistics, including the mean, the standard deviation, the min, and the max.

Note that we've done them all at once.  `df.mean()`, for example, computes the means of all the variables in one line.  Ditto the others.

Notice how pandas was smart and only tried to do compute these statistics for columns with numerical data (e.g. it skipped over the `country` column). This -- pandas doing intelligent things so our code "just works" -- is a theme we'll see many times over the coming weeks.

**Plotting.**  We have a number of methods available that plot DataFrames.  The most basic is the `plot()` method, which plots all of the variables against the index.  Try this and see what it looks like:

```python
df.plot()
```

You should see lines for each of the variables plotted against the index `name`.

Let's put what we've learned to work:

**Exercise.** Set `year` as the index and assign the result to the DataFrame `dfi`.  Use the `index` method to extract it and verify that `year` is, in fact, the index.

**Exercise.**  Apply the `reset_index()` method to our new DataFrame `dfi`.  What does it do?  What is the index of the new DataFrame?

**Exercise.** What kind of object is `df.mean()`?

**Exercise.** Copy the DataFrame `df` into an empty spreadsheet on your computer using the `to_clipboard()` method.

**Exercise.**  Produce a bar chart of `df` with the statement (Hint: use the docstring for `df.plot` to see what `kind` argument does)
