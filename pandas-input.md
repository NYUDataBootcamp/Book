# Pandas 1:  Data input

---
**Overview.**  We introduce "packages" -- collections of tools that extend Python's capabilities -- and explore one of them:  Pandas, the Python package devoted to data management.  We use Pandas to read spreadsheet data into Python and describe the "DataFrame" this produces.

**Python tools.**  Import, Pandas, reading spreadsheet files, DataFrames, series, columns, index.

**Buzzwords.**  Package, csv file, API.

**Applications.**  Income and output of countries, government debt, income by college major, old people, equity returns, George Clooney's movie roles.

**Code.**  [Link](https://raw.githubusercontent.com/NYUDataBootcamp/Materials/master/Code/Python/bootcamp_pandas-input.py).

---

We're ready now to look at some data.  Lots of data.  You will need an **internet connection** for much of it.

You may recall that our typical program consists of data input, data management, and graphics.  We'll spend most of our time here on the first -- data input -- but touch briefly on the second and third.  More concretely, we explain how to get spreadsheet data into Python.  We'll review how  Python uses collections of tools or plug-ins called **packages** to address a wide range of applications:  data management (**Pandas**), graphics (Matplotlib), and many other things.

The Pandas package is (even) more **[high-level](https://en.wikipedia.org/wiki/High-level_programming_language)** than core Python in the sense of putting a lot of the programming details out the way.  That makes it both easier to use -- lots of things are automated -- but in some cases also a bit more mysterious.  All together, though, it's an incredibly powerful collection of data tools.

## Reminders

* Objects and methods.  Recall that we apply the method `justdoit` to the object `x` with `x.justdoit()`.

* Help.  We get help in Spyder from both the IPython console and the Object inspector.  For the hypothetical `x.justdoit`, we would type `x.justdoit?` in the IPython console or `x.justdoit` in the Object inspector.

* Data structures.  That's the term we use for specific organizations of data.  Examples are lists, tuples, and dictionaries. Each has a specific structure and a set of methods we can apply.  List are (ordered) collections of objects between square brackets:  `numberlist = [1, -5, 2]`.  Dictionaries are (unordered) pairs of items between curly brackets:  `namedict = {'Dave': 'Backus', 'Chase': 'Coleman'}`. The first item in each pair is the "key," the second is the "value.""

* Integers, floats, and strings.  Three common types of data.

* Function returns.  We refer to the output of a function as its **return**.  We would say, for example, that the function `type(x)` `return`s the type of the input object `x`.  We capture the return with an assignment:  `xtype = type(x)`.

* Packages. Packages are collections of tools -- functions and types/methods -- that extend Python's capabilities. We import a package using an `import` (e.g. `import pandas`) statement or some combination of `import`, `from`, and `as` (e.g. `import pandas as pd` or `from pandas import DataFrame`).

## Data input 1:  reading internet files

The easiest way to get data into a Python program is to read it from a file -- a spreadsheet file, for example.  The word "read" here means take what's in the file and somehow get it into Python so we can do things with it.  Pandas can read many types of files:  csv, xls, xlsx, and so on.  The files can be on our computer or on the internet.  We'll start with the internet -- there's less ambiguity about the location of the file -- but the same approach works with files on your computer.


We prefer **csv files** ("comma separated values"), a common data format for serious data people.  Their simple structure (entries separated by commas) allows easy and rapid input. They also avoid some of [the problems](http://www.win-vector.com/blog/2014/11/excel-spreadsheets-are-hard-to-get-right/) with translating Excel files.  If we have an Excel spreadsheet, we can always save it as a "CSV (Comma delimited) (*.csv)" file.  Excel will warn us that some features are incompatible with the csv format, but we're generally happy to do it anyway.  Here's an example of a [raw csv file](https://raw.githubusercontent.com/NYUDataBootcamp/Materials/master/Data/test.csv) (pretty basic, eh?) and [this is](https://github.com/NYUDataBootcamp/Materials/blob/master/Data/test.csv) (roughly) how it's displayed in Excel.

<!--
  https://twitter.com/aejolene/status/700373933141401600
-->

**Reading csv files.** It's easy to read csv files with Pandas.  We'll read one from our GitHub repository to show how it works. We like to read data from internet sources like this, especially when the data is automatically updated at the source.  That's not the case here, but we'll see how easy it is to get this kind of data into Python.  We read the cleverly-named `test.csv` with the equally clever `read_csv` function in Pandas:

```python
import pandas as pd
url1 = 'https://raw.githubusercontent.com/NYUDataBootcamp'
url2 = '/Materials/master/Data/test.csv'
url  = url1 + url2        # location of file
df = pd.read_csv(url)     # read file and assign it to df
```

The syntax works like this:

* `url` is a string that tells Python where to look for the file.  We break it in two because it's too long to fit on one line.
* `read_csv()` is a Pandas function that reads csv files.  The `pd.` before it tells Python it's a Pandas function; we established the `pd` abbreviation in the `import` statement.
* The `df` on the left makes this an assignment:  We assign what we read to the variable `df`.


**Digression.** We won't do this often, but if the internet is down, or we want a simple example to experiment with, we can create data like this from a dictionary.  Each pair in this dictionary consists of a variable name (the "key") and a list containing data (the "value").  This code reproduces the output of the `read_csv` function above:

```python
df = pd.DataFrame({'name': ['Dave', 'Chase', 'Spencer'],
                   'x1': [1, 4, 5], 'x2': [2, 3, 6], 'x3': [3.5, 4.3, 7.8]})
```

This constructs a DataFrame from a dictionary.  In the dictionary, each "key" is a variable name expressed as a string and each "value" is a list that produces a column of data.  **End digression.**

So what does our read statement give us?  What's in `df`?  We can check its contents by adding the statement `print('\n', df)`.  (The `'\n'` tells the print function to start printing on a new line, which makes the output look better.)  The result is

```
      name  x1  x2   x3
0     Dave   1   2  3.5
1    Chase   4   3  4.3
2  Spencer   5   6  7.8
```

What we have is a table, much like what we'd see in a spreadsheet.  If we compare it to the [source](https://github.com/NYUDataBootcamp/Materials/blob/master/Data/test.csv) we see that the first column is new, added somehow by the program, but the others are just as they look in the source.

Note that the table of data has labels for both the columns and rows.  We'll do more with both of them shortly.

The documentation for `read_csv` in the Object inspector gives us an overwhelming amount of information.  Starting at the bottom, we see that it returns a **DataFrame**.  More on that shortly.  We also see a long list of optional inputs that change how we read the file.  Here are some examples we've found useful:

**Example.**  Change the last line of the earlier code to

```python
dfalt = pd.read_csv(url, nrows=2)
print('\n', dfalt)
```

The argument `nrows=2` tells the `read_csv` statement to read only the first 2 rows of the file at `url`.

**Example.**  We can identify specific values in a csv file as missing or NA (not available).  We see in the documentation that the parameter `na_values` takes a list of strings as input.  To treat the number 1 as missing we change the read statement to `read_csv(url, na_values=[1])`.  The result is

```python
      name  x1  x2   x3
0     Dave NaN   2  3.5
1    Chase   4   3  4.3
2  Spencer   5   6  7.8
```

We see that the number 1 that was formerly at the top of the `x1` column has been replaced by `NaN` -- "not a number". This particular example is somewhat silly, as we probably do not want to pretend that the number 1 is actually missing data. However, as we will see throughout the course, real data is messy and often has missing values. We've come across all these markers (and more) for noting that some data is missing: `-`, `null`, `n/a`, `NA`, `N/A`, `nan`, `NaN`, ... Being able to tell pandas which values to treat as missing will allow us to read in some otherwise troublesome data.

**Reading Excel files.** We can also read Excel files (xls and xlsx) with Pandas using the `read_excel()` function.  The syntax is almost identical:

```python
import pandas as pd
url1 = 'https://raw.githubusercontent.com/NYUDataBootcamp'
url2 = '/Materials/master/Data/test.xls'
url  = url1 + url2
dfx = pd.read_excel(url)
print('\n', dfx)
```

If all goes well, the modified code produces a DataFrame `dfx` that's identical to `df`.

**Exercise.**  Run the code

```python
url1 = 'https://raw.githubusercontent.com/NYUDataBootcamp'
url2 = '/Materials/master/Data/test0.csv'    # note the added 0
url  = url1 + url2
df = pd.read_csv(url)
```

What happens?  Why?

**Exercise.** Delete the `0` in `test0` and rerun the code.  What happens if you add the argument `index_col=0` to the `read_csv` statement?  How does `df` change?

**Exercise.** In the `read_excel` code, change the file extension at the end of `url2` from `.xls` to `.xlsx`.  What does the new code produce?

**Exercise.** Adapt the `read_csv` code to treat the numbers 1 and 6 as missing.  *Hint:* See the example a page or so back.

## Properties of DataFrames

Ok, so we read a file and assigned its contents to `df`.  But what is `df`?  What kinds of things can we do with it?

We start by finding its type.  We use the handy `type()` function and enter `type(df)` in the IPython console.  It responds:  `pandas.core.frame.DataFrame`.  More simply, it's a **DataFrame**.  A DataFrame is another example of a data structure, like a list or a dictionary, that organizes data in a specific way.  A DataFrame has three components:  a table of data, column labels, and row labels.

Typically columns are variables and the column labels give us their names.  In our example, the second column has the name `x1` and its values follow below it.  The rows are then observations, and the row labels give us their names.  This is a standard setup and we'll do our best to conform to it.  If the data come in some other form, we'll try to convert it.

**Dimensions.** We access a DataFrame's dimensions -- the numbers of rows and columns -- with the `shape` method:  `df.shape`.  Here the answer is `(3,4)`, so we have 3 rows (observations) and 4 columns (variables).

**Columns and indexes.**  We access the column and row labels directly.  For the DataFrame `df` we read in earlier, we extract column labels with the `columns` method:  `df.columns`.  That gives us the verbose output `Index(['name', 'x1', 'x2', 'x3'], dtype='object')`.  If we prefer to have them as a list, we use `list(df)`.  That gives us the column names as a list:  `['name', 'x1', 'x2', 'x3']`.  If we check the [source](https://github.com/NYUDataBootcamp/Materials/blob/master/Data/test.csv), we see that the column labels come from the first row of the file.

The row labels are referred to as the **index**.  We extract them by accessing `df.index`.  That gives us the verbose output `Int64Index([0, 1, 2], dtype='int64')`.  We can convert it to a list by adding another method, `df.index.tolist()`, which gives us `[0, 1, 2]`.  In this case, the index is not part of the original file; Pandas inserted a counter.  As usual in Python, the counter starts at zero.

**Column data types.**  Pandas allows every column (typically a variable) to have a different data type, but the type must be the same within a column.  With our DataFrame `df`, we get the types with the `dtypes` method; that is, with `df.dtypes`:

```python
name     object
x1        int64
x2        int64
x3      float64
```

Evidently `x1` and `x2` are integers and `x3` is a float.  They're no different from the types of numbers we came across in the previous chapter.  The first column, `name`, is different.  Object is the name Pandas gives to things it can't turn into numbers -- in our case, strings.  Sometimes, as here, that makes sense:  names like `Dave` and `Spencer` are naturally strings.  But in many cases we've run across, numbers are given the dtype object because there was something in the data that didn't look like a number.  We'll see more of that later on.

**Transpose columns and rows.** If we want to rotate the DataFrame, exchanging columns and rows, we use the `transpose` method:  `df.transpose` or (more succinctly) `df.T`.  Let's do that with the DataFrame `df` we read in earlier:

```python
dft = df.T
print('\n', dft)
```

The result is

```
         0      1        2
name  Dave  Chase  Spencer
x1       1      4        5
x2       2      3        6
x3     3.5    4.3      7.8
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


## Working with variables

So we have a DataFrame `df` whose columns are variables.  One of the great things about Pandas is that we can do things with every observation of a variable in one statement.

**Variables = series.**  In the DataFrame `df` we created earlier, if we want to refer to the variable `x1` we write `df['x1']`.  If we ask what type this is, with

```python
print(type(df['x1']))
```

we find that it's a `pandas.core.series.Series` -- **series** for short.  A series is essentially a DataFrame with a single variable or column, which simplifies the bookkeeping a bit.


**Construct new variables from old ones.** Now that we know how to refer to a variable, we can construct others from them.  We construct two with

```python
df['y1'] = df['x1']/df['x2']
df['y2'] = df['x2'] + df['x3']
```

The first line computes the new variable `y1` as the ratio of `x1` to `x2`.  The second computes `y2` as the sum of `x2` and `x3`.

These statements do two things:  they perform the calculation on the right, and they assign it to the variable on the left.  The second step adds the new variables to the DataFrame.  The statement `print('\n', df)` now gives us

```python
       name  x1  x2   x3        y1    y2
0     Dave   1   2  3.5  0.500000   5.5
1    Chase   4   3  4.3  1.333333   7.3
2  Spencer   5   6  7.8  0.833333  13.8
```

If we step back for a minute, we might compare this to Excel.   If `x2` and `x3` are columns, then we might start a new column labeled `y2`.  We would then compute the value of `y2` for the first observation and copy the formula to the other observations.  Here one line of code computes them all.


**Digression.** There are two syntax issues we should mention.  One is that others -- not us! -- commonly refer to a variable `df[`y1`]` by `df.y1`.  That usually works, but not always.  For example, it doesn't work if the variable name contains spaces or conflicts with an existing method.  And we can't assign to it, as we did when we defined `y1` above.  The second issue is integer variable names.  We avoid these, too, but if we somehow end up with a variable with an integer label -- `2011`, for example -- we would refer to it by that label: `df[2011]` without quotes.  If you're not sure what type the variable labels are, print `df.columns` and see whether they have quotes.


**Rename variables.**  If we want to change *all the names*, we can assign a list of new names to the DataFrame's column labels:

```python
df.columns = ['NAME', 'X1', 'X2', 'X3']
```

Here we've simply changed the column names to upper case.  There's a clever way to do this with a list comprehension:

```python
df.columns = [var.upper() for var in df.columns]
```

The flexibility of string methods and list comprehensions opens up a lot of possibilities.

We can also assign new names individually.  Suppose we want to give `x1` the more intuitive name `sales`.  We can do that with the statement

```python
df.rename(columns={'x1': 'sales'})
```

Note the use of a dictionary that associates the old name (the "key" `x1`) with the new name (the "value" `sales`).  If we want to change more than one variable name, we simply add more items to the dictionary.


**Extract variables.**  We just saw that `df['x1']` "extracts" the variable/series `x1` from the DataFrame `df`.  In other cases, we may want to extract a set of variables and create a smaller DataFrame.  This happens a lot when our data has way more variables than we need.

We can extract variables by name or number.  If by name, we simply put the variable names in a list.  If by number, we count (as usual) starting with zero.  This code gives us two ways to extract `x1` and `x3` from `df`:

```python
namelist = ['x1', 'x3']
numlist  = [1, 3]
df_v1 = df[namelist]
df_v2 = df[numlist]
```

You might verify that the two new DataFrames are identical.

Closely related is the `drop` method.  If we want to drop the variable `x2`, we would use

```python
df.drop(['x2'], axis=1)
```

Here `axis=1` refers to columns; `axis=0` refers to rows.


**Exercise.**  For the DataFrame `df`, create a variable `z` equal to the sum of `x1`, `x2`, and `x3`.  Verify that `z` is now in `df`.


**Exercise.** How would you extract the variables `x1` and `x2`?


**Exercise.** How would you drop the variable `z`?


**Exercise (very challenging).** Use a list comprehension to change the variable names from `['x1', 'x2', 'x3']` to `['y1', 'y2', 'y3']`.  *Hint:*  What does `s.replace('x', 'y')` do to the string `s = "xray"`?


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


**Setting the index.**  We're not stuck with the index in our DataFrame, we can make it whatever we want.  If we want to use `name` as the index, associating observations with the `name` variable, we use the `set_index()` method:

```python
df = df.set_index(['name'])
```

That gives us

```python
         x1  x2   x3        y1    y2
name
Dave      1   2  3.5  0.500000   5.5
Chase     4   3  4.3  1.333333   7.3
Spencer   5   6  7.8  0.833333  13.8
```

with `name` now used as the index.

We did something else here that's important:  We assigned the result back to `df`.  That keeps what we've done in the DataFrame `df`.  If we hadn't done this, `df` would remain unchanged with a counter as its index and our effort to set the index would be lost.

We can reverse what we did here with the `reset_index()` method:

```python
df_reset = df.reset_index()
```

Try it and see.  We'll spend more time on these methods in a couple weeks.


**Statistics.**  We can compute the mean, the standard deviation, and other statistics for all the variables at once with

```python
df.mean()
df.std()
df.describe()
```

The first line gives us the means, the second the standard deviations.  The third line gives us a collection of statistics, including the mean, the standard deviation, the min, and the max.

Note that we've done them all at once.  `df.mean()`, for example, computes the means of all the variables in one line.  Ditto the others.

Notice how pandas was smart and only tried to do compute these statistics for columns with numerical data (e.g. it skipped over the `name` column). This -- pandas doing intelligent things so our code "just works" -- is a theme we'll see many times over the coming weeks.


**Plotting.**  We have a number of methods available that plot DataFrames.  The most basic is the `plot()` method, which plots all of the variables against the index.  Try this and see what it looks like:

```python
df.plot()
```

You should see lines for each of the variables plotted against the index `name`.

Let's put what we've learned to work:


**Exercise.** Set `name` as the index and assign the result to the DataFrame `dfi`.  Use the `index` method to extract it and verify that `name` is, in fact, the index.

**Exercise.**  Apply the `reset_index()` method to our new DataFrame `dfi`.  What does it do?  What is the index of the new DataFrame?

**Exercise.** What kind of object is `df.mean()`?

**Exercise.** Copy the DataFrame `df` into an empty spreadsheet on your computer using the `to_clipboard()` method.

<!--
**Exercise.** The statement `print(df.mean())` gives us the means of each variable in a column.  How would we produce the same output as a row?
-->

**Exercise.**  Produce a bar chart of `df` with the statement (Hint: use the docstring for `df.plot` to see what `kind` argument does)


## Data input 2:  Reading files from your computer

Next up:  reading files in Python from your computer's hard drive.  This is really useful, but there's a catch:  we need to tell Python where to find the file.


**Prepare test data.**  We start with the easy part.  Open a blank spreadsheet in Excel and enter the data:

```
name    x1  x2   x3
Dave     1   2  3.5
Chase    4   3  4.3
Spencer  5   6  7.8
```

That is:  four rows with four entries in each one.

Now save the contents in your `Data_Bootcamp` directory.  Do this three times in different formats:

* Excel file.  Save the file as `test.xlsx`.
* Old-style Excel file.  Save as an "Excel 97-2003 (*.xls)" file under the name `test.xls`.
* CSV file.  Save as a "CSV (Comma delimited) (*.csv)" file under the name `test.csv`.

Each of these options shows up in Excel when we choose "Save As."


**Find the file.**  Ok, now where is the file?  We know, it's in the `Data_Bootcamp` directory, but where is that?  We need the complete path so we can tell Python where to find it.


**Exercise (potentially challenging).** We can save some time if you already know this.  (It's not required, we're just giving it a shot.)  Find the path to `test.csv` on your computer.  If you find it, tell us what you did.  If you're not sure what this means, or how to do it, raise your hand.


Let's introduce some terms so we can be clear what we're talking about.  The "file name" is something like `test.csv`.  The format of the "directory" or folder address depends on the operating system.  On a Windows computer, it's something like

```
C:\Users\userid\Documents\Data_Bootcamp
```

On a Mac, it looks like

```
/Users/userid/Data_Bootcamp
```

The complete path to the file `test.csv` is a combination of the path to the directory and the file name, with a slash in between.  In Windows:

```
C:\Users\userid\Documents\Data_Bootcamp\test.csv
```

In Mac OS:

/Users/userid/Data_Bootcamp/test.csv
```

Note that they use different kinds of slashes.

How did we find these addresses or paths?

* Windows.  Type the name of the file in the Windows search box or use Windows Explorer.
* Mac OS.  We select (but not open) the file and do "command-i" to get the file's information window.  From the window, we copy the path that follows "Where:."  It looks like we're copying arrows, but they turn into slashes when we paste the path.

[Comments welcome on how to make this clearer.]

**Reading data with the complete path.**  Once we have the complete path, we simply tell Python to read the file at that location.  Again, this varies with the operating system.

* In Windows, we take the complete path and -- **this is important** -- change all the backslashes `\` to either double backslashes `\\` or forward slashes `/`.  (Don't ask.)  Then we read the file from the path, just as we read it from a url earlier:

```python
path = 'C:\\Users\\userid\\Documents\\Data_Bootcamp\\test.csv'
df = read_csv(path)
```

* In Mac OS we don't need to change the slashes:

```python
path = '/Users/userid/Data_Bootcamp/test.csv'
df = read_csv(path)
```

* In both:  Open the file in Excel, click on File, and read the path from the Info tab.


**Exercise.** Read `test.csv` using the path and the method described above.  Let us know if you have trouble.


**Reading from the current working directory.** An alternative is to set the current working directory (cwd), which is where Python will look for files.  We can set that with Python's [os module](https://docs.python.org/3.5/library/os.html).  What you'll need is the location of the `Data_Bootcamp` directory.

Once we know the directory path, we can use it in Python.

* In Windows, we use

  ```python
  import os

  file = 'test.csv'
  cwd  = 'C:/Users/userid/Data_Bootcamp'

  os.chdir(cwd)                                 # set current working directory
  print('Current working directory is', os.getcwd())
  print('File exists?', os.path.isfile(file))   # check to see if file is there

  df = pd.read_csv(file)
  ```

<!--
http://www.howtogeek.com/181774/why-windows-uses-backslashes-and-everything-else-uses-forward-slashes/
-->

* In Mac OS, the only difference is the format of the path:

  ```python
  import os

  file = 'test.csv'
  cwd  = '/Users/userid/Data_Bootcamp'

  os.chdir(cwd)                                 # set current working directory
  print('Current working directory is', os.getcwd())
  print('File exists?', os.path.isfile(file))   # check to see if file is there

  df = pd.read_csv(file)
  ```

Once we've set the path, we read the csv file as before.  `read_excel()` works the same way with Excel files.

<!--
**Reading from the current working directory.** An alternative is to set the current working directory (cwd).  How we do that depends on our environment, which is why we prefer the other approach:  It works in all environments.  In Spyder, the path of the cwd is in a textbox at the top on the right side.  (Take a look, make sure you can find it.)  If the cwd is where our data file is, skip the next part.  If not, we can reset it in two steps:

* Find the folder icon to the right of the cwd textbox.  We know we have the right one if a text bubble pops up that says "Browse a working directory".  Click on the icon and navigate to the folder/directory that contains our data file, namely `Data_Bootcamp`.  Then click on "Select Folder" to choose it.

* Next we click on the red arrow to the right of the folder icon, the one with the text bubble that says "Set as current console's working directory".  That should set the cwd to `Data_Bootcamp`.

Once this is done, we can read the file with
```python
file = 'test.csv'
df = read_csv(file)
```
If this doesn't work, go back to the complete path.
-->


**Report problems.**  If you have difficulty, or find that this works differently on your computer, let us know.


## Data input:  Examples

Here are some spreadsheet datasets we find interesting.  In each one, we describe the data using the `shape`, `columns`, and `head()` methods.  Where we can, we also produce a simple plot.

At this point you should **download the code file** for this chapter, linked on the first page (the top of this page if you are viewing online).  Save it in your `Data_Bootcamp` directory and open it in Spyder.  That will save you a lot of typing.

**Penn World Table.**  The [PWT](http://www.rug.nl/research/ggdc/data/pwt/?lang=en), as we call it, is a standard database for comparing the incomes of countries.  It includes annual data for GDP, GDP per person, employment, hours worked, capital, and many other things.  The variables are measured on a comparable basis, with GDP measured in  2005 US dollars.

The data is in an [Excel spreadsheet](http://www.rug.nl/research/ggdc/data/pwt/v81/pwt81.xlsx).  If we open it, we see that it has three sheets.  The third one is the data and is named `Data`.  We read it in with the code:

```python
url = 'http://www.rug.nl/research/ggdc/data/pwt/v81/pwt81.xlsx'
pwt = pd.read_excel(url, sheetname='Data')
```

So what does that give us?

* `pwt.shape` returns `(10357, 47)`:  the DataFrame `pwt` contains 10,357 observations of 47 variables.
* `list(pwt)` gives us the variable names, which include `countrycode`, `country`, `year`, `rgdpo` (real GDP), and `pop` (population).
* `pwt.head()` shows us the first 5 observations, which refer to Angola for the years 1950 to 1954.  If we look further down, we see that countries are stacked on top of each other in alphabetical order.

In this dataset, each column is a variable and each row is an observation.  But if we were to plot one of the variables, it wouldn't make much sense.  The observations string together countries, one after the other.  What we'd like to do is compare countries, which this isn't set up to do -- yet.


**Exercise.** Download the spreadsheet and open it in Excel.  What does it look like?  (You can use your Google fu here:  Google "penn world table 8.1", go to the first link, and look for the Excel link.)

**Exercise.** Change the input in the last line of code to `sheetname=2`.  Why does this work?

**World Economic Outlook.**  Another good source of macroeconomic data for countries is the IMF's [World Economic Outlook](https://www.imf.org/external/ns/cs.aspx?id=28) or WEO.  It comes out twice a year and includes annual data from 1980 to roughly 5 years in the future (forecasts, evidently).  It includes the usual GDP, but also government debt and deficits, interest rates, and exchange rates.

This one gives us some idea of the challenges we face dealing with what looks like ordinary spreadsheet data.  The file extension is `xls`, which suggests it's an Excel spreadsheet, but that's a lie.  In fact it's a "tab-delimited" file:  essentially a csv, but with tabs rather than commas separating entries.  We read it with

```python
url1 = 'https://www.imf.org/external/pubs/ft/weo/'
url2 = '2015/02/weodata/WEOOct2015all.xls'
weo = pd.read_csv(url1+url2,
                  sep='\t',                 # \t = tab
                  thousands=',',            # kill commas
                  na_values=['n/a', '--'])  # missing values
```

This has several features we need to deal with:

* Use `read_csv()` rather than `read_excel()`:  it's not an Excel file despite what the file name suggests
* Identify tabs as the separator between entries with the argument `sep='\t'`.
* Use the `thousands` argument to eliminate commas from numbers -- things like `12,345.6`, which Python will treat as strings.  (What were they thinking of?)
* Identify missing values with the `na_values` argument.

Keep in mind that it took us an hour or two to figure all this out.  You can get a sense of where we started by running the `read_csv` statement without the last two arguments and listing its dtypes.  You'll notice that variables you might expect to be floats are objects instead.


**Exercise.** Download the WEO file.  What happens when you open it in Excel?  (You can use the link in the code.  Or Google "imf weo data", look for the most recent link, and choose Entire Dataset.)

**Exercise.**  Why were we able to spread the `read_csv()` statement over several lines?

**Exercise.**  Google "python pandas weo" to see if someone else has figured out how to read this file.

**Exercise.** How big is the DataFrame `weo`?  What variables does it include?  Use the statement `weo[[0, 1, 2, 3, 4]].head()` to see what the first five columns contain.


This dataset doesn't come in the standard format, with columns as variables and rows as observations.  Instead, each row contains observations for all years for some variable and country combination.  If we want to work with it, we'll have to change the structure. Which we'll do, but not now.

<!--
**Historical government debt data.** The IMF also has an informal release that covers the complete [history of government debt](http://www.imf.org/external/ns/cs.aspx?id=262), or at least as much of it as we have data for.  We'll use it to plot the ratio of government debt to GDP for the UK and Greece.

We read the data

Plot debt ...
-->


**PISA education data.**  PISA stands for [Program for International Student Assessment](http://www.oecd.org/pisa/).  It's an international effort to collect information about educational performance that's comparable across countries.  We read about it every few years when newspapers print stories about how poorly American students are doing.  PISA collects data on student test performance, teacher quality, and many other things, and posts both summaries and individual test results.

We use data from a summary table in an [OECD report](http://www.oecd.org/pisa/keyfindings/pisa-2012-results-volume-I.pdf); note the data link at the bottom of Table 1.A.  This code reads the data from the link:

```python
url = 'http://dx.doi.org/10.1787/888932937035'
pisa = pd.read_excel(url,
                     skiprows=18,             # skip the first 18 rows
                     skipfooter=7,            # skip the last 7
                     parse_cols=[0,1,9,13],   # select columns of interest
                     index_col=0,             # set the index as the first column
                     header=[0,1]             # set the variable names
                     )
```

There are a number of new things in the read statement:

* We spread the read statement over several lines to make it easier to read.  Python understands that the line doesn't end until we reach the right paren `)`.  That's common Python syntax.
* We skip rows at the top and bottom that do not contain data.
* We choose specific columns to read using the `parse_cols` parameter.  Column numbering starts at zero, as we have come to expect. Here we select the mean score for each field (math, reading, science).
* We set the index as the first column.
* We set the header from the first two rows (after those we skip).  Note that the header has two parts:  the field (math, reading, science) and the measurement (mean, share of low-achievers, etc).

We can clean this up further if we drop blank lines and simplify the variable names:

```python
pisa = pisa.dropna()                            # drop blank lines
pisa.columns = ['Math', 'Reading', 'Science']   # simplify variable names
pisa['Math'].plot(kind='barh')
```

The plot we produce in the last line is virtually impossible to read, but we'll work on that later.

**UN population data.**  We tend to have pretty good demographic data.  We keep track of how many people we have, their ages, how many children they have, what they die of, and so on.  A good international source is the [United Nations' Population Division](http://esa.un.org/unpd/wpp/Download/Standard/Population/).

This code reads in estimates of population by age for many countries:

```python
url1 = 'http://esa.un.org/unpd/wpp/DVD/Files/'
url2 = '1_Indicators%20(Standard)/EXCEL_FILES/1_Population/'
url3 = 'WPP2015_POP_F07_1_POPULATION_BY_AGE_BOTH_SEXES.XLS'
url = url1 + url2 + url3

cols = [2, 4, 5] + list(range(6,28))
est = pd.read_excel(url, sheetname=0, skiprows=16, parse_cols=cols)
```

The columns contain population numbers for 5-year age groups.  When we're up to it, we'll use this data to illustrate the dramatic aging of the population in many countries.  It's one of the striking facts of modern times:  people are living longer, a lot longer.


**Exercise.** What does `list(range(6,28))` do?  Why?


**Incomes by college major.** Nate Silver's [538 blog](http://fivethirtyeight.com/) does a lot of good data journalism and often posts its data online.  This one comes from their analysis of [income by college major](http://fivethirtyeight.com/features/the-economic-guide-to-picking-a-college-major/).  The data comes from the American Community Survey but they've done the work of organizing it for us.

Here's the code:

```python
url1 = 'https://raw.githubusercontent.com/fivethirtyeight/data/master/'
url2 = 'college-majors/recent-grads.csv'
url = url1 + url2
df538 = pd.read_csv(url)
```

**Exercise.** What variables does this data contain?

**Exercise.** Set the index as `Major`.  (Ask yourself:  What method should I use?)

**Exercise.** Create a horizontal bar chart with the variable `Median` (median salary) using the `plot()` method.


**Internet Movie Database (IMDb).**  We love this one, a list of roles in IMDb's movie database we got from [Brandon Rhodes](https://github.com/brandon-rhodes/pycon-pandas-tutorial).  We read it with this code:

```python
url  = 'http://pages.stern.nyu.edu/~dbackus/Data/cast.csv'
cast = pd.read_csv(url, encoding='utf-8')
```

Don't panic if nothing happens for a while.  It's a big file (approximately 200 MB) and takes a minute or two to read.

**Exercise.** Since we're all experts by now, we'll leave this one to you:

* How large is the DataFrame?
* What variables does it include?
* Try these statements:

   ```python
   ah = cast[cast['title'] == 'Annie Hall']
   gc = cast[cast['name'] == 'George Clooney']
   ```

This goes beyond what we've done so far, but what do you think they do?  What do the DataFrames `ah` and `gc` contain?

<!--
**Healthcare by location.**
http://www.nytimes.com/interactive/2015/12/18/upshot/19up-healthcosts.html
http://www.nytimes.com/interactive/2015/12/15/upshot/the-best-places-for-better-cheaper-health-care-arent-what-experts-thought.html

**Heart attack data.**
```python
https://data.medicare.gov/api/views/c7us-v4mf/rows.csv?accessType=DOWNLOAD
https://data.medicare.gov/developers
"""
import pandas as pd
url = 'https://data.medicare.gov/api/views/c7us-v4mf/rows.csv'
df = pd.read_csv(url)
```

**Example (Airbnb).** Chase likes this one.  Someone posted a bunch of Airbnb data online.

http://insideairbnb.com/get-the-data.html

-->

<!--
**Example (Stern teaching data).**


**Example.** Chetty's income data...

**Example (Big Mac currency index).**  This is an xls file with multiple sheets.
http://infographics.economist.com/2015/databank/BMfile2000-Jul2015.xls

https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/27893

Papers:  https://scholar.google.com/scholar?hl=en&q=fisman+speed+dating&btnG=&as_sdt=1%2C33
-->


<!--
**Example (Chipotle).**

**Example (Reinhart-Rogoff).**

http://simplystatistics.org/2013/04/16/i-wish-economists-made-better-plots/


**Example (AirBNB).**

http://insideairbnb.com/get-the-data.html

**Example (mortality).** Causes from CDC...


**Example (bond yields).**


**Example (speed dating).**  download tab delimited data and read it with `read_csv`.

**Example.** Beer ratings...
https://github.com/TomAugspurger/PyDataSeattle/blob/master/notebooks/3.%20Indexing.ipynb
-->


## Data input 3:  APIs


APIs are "application program interfaces".  That's a mouthful.  A dataset with an API allows access through some method other than a spreadsheet.  The API is the set of rules for accessing the data.  The bad news is the jargon.  The good news is that people have written easy-to-use code to access the APIs.  We don't need to understand the API, we just use the code -- and say thank you!

The Pandas package has what they call a set of [Remote Data Access tools](http://pandas.pydata.org/pandas-docs/stable/remote_data.html).  They break now and then, typically when the underlying data changes, but when they work they're great.  This part of Pandas is undergoing a transition, but for now this is how it works.


**FRED.** The St Louis Fed has put together a large collection of time series data that they refer to as [FRED](https://research.stlouisfed.org/fred2/):  Federal Reserve Economic Data.  They started with the US, but now include data for many countries.

The Pandas docs describe how to access FRED.  Here's an example that reads in quarterly data for US real GDP and real consumption and produces a simple plot:

```python
import pandas.io.data as web    # package to access FRED
import datetime                 # package to handle dates

start = datetime.datetime(2010, 1, 1)  # start date
codes = ['GDPC1', 'PCECC96']    # real GDP, real consumption
fred  = web.DataReader(codes, 'fred', start)
fred = fred/1000                # convert billions to trillions

fred.plot()
```

We copied most of this from the Pandas documentation.  Which is a good idea:  Start with something that's supposed to work and change one thing at a time until you have what you want.

The variable `start` contains a date in (year, month, day) format. Pandas knows a lot about how to work with dates, especially when we construct them using `datetime.datetime` as we did above. We're hoping to cover pandas' time series capabilities in depth in a future chapter of the book.

The variable `codes`  -- not to be confused with "code" -- consists of FRED variable codes.  Go to [FRED](https://research.stlouisfed.org/fred2/), use the search box to find the series you want, and look for the variable code at the end of the url in your browser.

<!--
click on the "Cite" tab below the figure, and look for the code in square brackets.
-->

**Exercise.** Run the same code with a start date of 2005.  What do you see?


**World Bank.** The World Bank's [databank](http://data.worldbank.org/) covers economic and social statistics for most countries in the world.  Variables include GDP, population, education, and infrastructure.  Here's an example:

```python
from pandas.io import wb            # World Bank api

var = ['NY.GDP.PCAP.PP.KD']         # GDP per capita
iso = ['USA', 'FRA', 'JPN', 'CHN', 'IND', 'BRA', 'MEX']  # country codes
year = 2013
wbdf = wb.download(indicator=var, country=iso, start=year, end=year)
```

If we look at the DataFrame `wbdf`, we see that it has a double index, `country` and `year`.  By design, all of the data is for 2013, so we kill off that index with the `reset_index` method and plot what's left as a horizontal bar chart:

```python
wbdf = wbdf.reset_index(level='year', drop=True)
wbdf.plot(kind='barh')
```

(Trust us on the `drop=True`.  We'll come back to it in a couple weeks.)

We use codes here for countries and variables.  We can find country codes in [this list](http://www.countryareacode.net/) -- or just Google "country codes".  Pandas accepts both 2- and 3-letter versions.  We find variable codes with the search tool in the Remote Data Access module or by looking through the World Bank's [data portal](http://databank.worldbank.org/data/home.aspx).  We prefer the latter.  Click on a variable of interest and read the code from the end of the url.


**Exercise.** What would you like to change in this graph?  Keep a list for the next time we run into this one.


**Fama-French.**  Gene Fama and Ken French post lots of data on equity returns on [Ken French’s website](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html).  The data are zipped text files, which we can easily read into Excel.  The Pandas tool is even better.  Here's an example:

```python
import pandas.io.data as web

ff = web.DataReader('F-F_Research_Data_factors', 'famafrench')[0]
ff.columns = ['xsm', 'smb', 'hml', 'rf']      # rename variables

ff.describe()
```

The data is monthly, 1926 to present.  Returns are expressed as percentages; multiply by 12 to get annualized returns.  The variable names refer to

* `xsm`:  the return on the market minus the riskfree return
* `smb`:  the return on small firms minus the return on big firms
* `hml`:  the return on value firms minus the return on growth firms
* `rf`:  the riskfree rate

We use the `describe()` method to compute statistics.  Evidently `xsm` has the largest mean.  It also has the largest standard deviation.  A couple plot methods show us more about the distribution:

```python
ff.boxplot()
ff.plot()
ff.plot(ff['xsm'], ff['smb'], kind='scatter')
```

What do you see?  What more would you like to know?


## Review

Run this code to create a DataFrame of technology indicators from the World Bank for four African countries:

```python
import pandas as pd
data = {'EG.ELC.ACCS.ZS': [53.2, 47.3, 85.4, 22.1],    # access to elec (%)
        'IT.CEL.SETS.P2': [153.8, 95.0, 130.6, 74.8],  # cell contracts per 100
        'IT.NET.USER.P2': [11.5, 12.9, 41.0, 13.5],    # internet access (%)
        'Country': ['Botswana', 'Namibia', 'South Africa', 'Zambia']}
af = pd.DataFrame(data)
```

(You can cut and paste this from the bottom of this chapter's code file.)

**Exercise.** What type of object is `af`?  What are its dimensions?

**Exercise.** What is the index?  Change it to country names.

**Exercise.** What are the variable names?  Change them to something more informative.

**Exercise.** Create a horizontal bar chart with this DataFrame.  What does it tell us?  Which country has the most access to electricity?  Cell phones?


## Resources

We've covered a lot of ground, but if you're looking for more we suggest:

* On Pandas:  Chris Moffitt's [Practical Business Python blog](http://pbpython.com/archives.html) has a good series on Pandas from the perspective of an Excel user.  For a more concise summary, try [Quandl's cheatsheet](https://s3.amazonaws.com/quandl-static-content/Documents/Quandl+-+Pandas%2C+SciPy%2C+NumPy+Cheat+Sheet.pdf).
* On data:  See the list of [data sources](http://databootcamp.nyuecon.com/bootcamp_data/) on the [course website](http://databootcamp.nyuecon.com/).
* On backslashes (and other obscure characters in code):  [xkcd](http://xkcd.com/1638/).


<!--
* Brandon Rhodes' exceptionally good [PyCon video](https://github.com/brandon-rhodes/pycon-pandas-tutorial).  Two and a half hours will rarely be better spent.

* xlrd:  http://tech.novus.com/augmenting-your-excel-workflow-with-python/  In Anaconda.  See [here](https://www.reddit.com/r/Python/comments/3fbdur/augmenting_your_excel_workflow_with_python/) for comments on similar packages.  Several of them, including xlrd, are in [Anaconda](http://docs.continuum.io/anaconda/pkg-docs).

https://realpython.com/blog/python/working-with-large-excel-files-in-pandas/

Kaggle example:  http://blog.kaggle.com/2013/01/17/getting-started-with-pandas-predicting-sat-scores-for-new-york-city-schools/

Chipotle data from NYT:
http://www.nytimes.com/interactive/2015/02/17/upshot/what-do-people-actually-order-at-chipotle.html?_r=0
https://raw.githubusercontent.com/TheUpshot/chipotle/master/orders.tsv
http://www.danielforsyth.me/pandas-burritos-analyzing-chipotle-order-data-2/

http://pandas.pydata.org/pandas-docs/stable/cookbook.html#data-in-out
http://pandas.pydata.org/pandas-docs/stable/io.html

History of debt (see data link on left):  http://www.imf.org/external/ns/cs.aspx?id=262

http://www.gregreda.com/2013/10/26/intro-to-pandas-data-structures/

Cookbook:  http://pandas.pydata.org/pandas-docs/stable/tutorials.html#pandas-cookbook

Pandas plotting methods:  http://pandas.pydata.org/pandas-docs/version/0.10.1/visualization.html#autocorrelation-plot
-->
