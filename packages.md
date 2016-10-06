# Python packages


---
**Overview.**  We introduce "packages" -- collections of tools that extend Python's capabilities. We describe tools used to update and install Python packages.

**Python tools.**  packages, Conda, Pip.

**Buzzwords.**  Command line.

**Applications.**  Seaborn, Bokeh, pandas-datareader, plotly

---

Python is not just a programming language, it's an open source collection of tools that includes both core Python and a large collection of packages written by different people.  The word **package** here refers to plug-ins or extensions that expand Python's capabilities.  Terminology varies.  What we call a package others sometimes call a "library."  The term "module" typically refers to a subset of core Python or one of its packages.  You won't go far wrong to use the terms interchangeably.

The standard Python packages are well written, well documented, and well supported.  They have armies of users who spot and correct problems.  Some of the others less so.  For the most part, we stick to the standard packages, specifically those that come with the Anaconda distribution.

Some of the leading packages for numerical ("scientific") computation are

* **[Pandas](http://pandas.pydata.org/).**  The leading package for managing data

* **[Matplotlib](http://matplotlib.org/).**  The leading graphics package.  We'll use it extensively.

* **[NumPy](http://www.numpy.org/).**  Tools for numerical computing.  In Excel the basic unit is a cell, a single number.  In NumPy the basic unit is a vector (a column) or matrix (a table or worksheet), which allows us to do things with an entire column or table in one line.  This facility carries over to Pandas.

All of these packages come with the [Anaconda distribution](http://docs.continuum.io/anaconda/pkg-docs.html), which means we already have them installed and ready to use.

Pandas is an essential part of data work in Python.  Its [authors describe it](http://pandas.pydata.org/) as "an open source library for high-performance, easy-to-use data structures and data analysis tools in Python."  That's a mouthful.  Suffice it to say that we can do pretty much everything in Pandas that we can do in Excel -- and more.  We can compute sums of rows and columns, generate new rows or columns, construct pivot tables, and lots of other things.  And we can do all this with much larger files than Excel can handle.

**More than you need**

Here are some other packages you might run across:

* **[Seaborn](http://stanford.edu/~mwaskom/software/seaborn/).** A "wrapper" (isn't that a great term?) for Matplotlib that makes it easier to use.

* **[Statsmodels](https://pypi.python.org/pypi/statsmodels).**  The basic statistics package -- This allows us to do things like regression.

* **[Scikit-learn](http://scikit-learn.org/stable/).** A package for "[machine learning](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/)," which is the name computer scientists give to data work.  CS people have done some cool things with data.  They're also really good at naming things:  machine learning, visualization, support vector machines, random forests.

* **[NLTK](http://www.nltk.org/).**  The so-called Natural Language Toolkit processes text.  Here "natural language" means "words."  Investors, for example, might process the words used in financial reports to detect mood or sentiment.  One of our students is using NLTK to analyze tweets.  The big-picture idea is that data can be anything, not just numbers.

* **[Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/)** and **[Scrapy](http://scrapy.org/).**  Extract ("scrape") data from web sites.

* **[Django](https://www.djangoproject.com/).**  A popular tool for website development.

We won't use most of them them, but they're in Anaconda too.  Feel free to give them a try.  If you do, please report back on your experience.

## Importing packages

In Python we need to tell our program which packages we plan to use.  We do that with an `import` statement.

Here are some examples applied to a mythical package `xyz` and mythical function `foo`:

* `import xyz`.  This imports the package `xyz`. A function `foo` in package `xyz` is then executed with `xyz.foo()`

* `import xyz as x`.  This also imports the package `xyz`, but under the abbreviation `x`.  Here `foo` is executed with `x.foo()`.  This is the most common syntax and the one we'll generally use.  With Pandas, for example, the standard import statement is `import pandas as pd`.

* `from xyz import foo`.  This imports the `foo` function directly so it can be called with `foo()`. Note in this case that if we had another function `bar` in the `xyz` package we wouldn't not be able to call it without importing the `bar` function like we did `foo`, or imported the `xyz` module itself using one of the methods above.

* `from xyz import *`.  This imports all the functions and methods from the package `xyz`, but here the function `foo` is executed simply by typing `foo`.  We don't usually do this, because it opens up the possibility that the same function exists in more than one package, which is virtually guaranteed to create confusion.

We'll see these examples repeatedly:

```python
import pandas as pd                  # data package
import matplotlib.pyplot as plt      # graphics package
```

You might also go through earlier chapters and identify the `import` statements you find.  By convention, they are placed at the top of the program.  What packages or modules have we used?  What do they do?

Some fine points:

* Redundancy.  What happens if we issue an import statement twice?  Answer:  Nothing, no harm done.

* Jokes.  These are programmer jokes, which some might see as a contradiction, but try them and see what happens:

  ```python
  import this
  ```

  ```python
  import antigravity
  ```

* Versions.  We can check the version number of a package with  `package.__version__`.  To check the version of Pandas you have installed, try

  ```python
  import pandas as pd
  print('Pandas version ', pd.__version__)   	# these are double underscores
  ```

  This can be helpful if we're trying to track down an error.


**Exercise.**  Import Pandas.  What version do you have?

**Exercise.**  What happens if we import Pandas twice under different names, once with `import pandas as pd` and once with `import pandas as pa`?  Write a short program that tests your conjecture.  *Hint:* Use what have we done with Pandas so far.


## Updating Python:  Conda and Pip


**Warning:  This is a little terse, but we think it does the trick.**

Python has some handy tools for installing and updating the core language and its packages.  We start with **conda**, the tool used to update the components of the Anaconda distribution, then move on to the traditional Python tool, **pip** (acronym for "pip installs packages").

As usual, the idea is to get things started.  We provide links to more extensive documentation at the end.

These tools run on the **command line**, the old-school approach to computing that predates the graphical interfaces we use today (Mac OS, Windows, etc).  Picture the computer screens in "[War Games](http://pc-museum.com/046-imsai8080/wargames.htm)."  Many of the graphical interfaces used in the computing world run things on the command line behind the scenes, so it's often better to go straight to the source and run things on the command line ourselves.

We have been doing this to open spyder, so we should have an idea of how to do this.

### Conda

Conda is the Anaconda tool.  We use the Anaconda distribution of Python, which we think is the most user-friendly version out there.  It comes with a variety of packages installed, including our favorites:  Pandas and Matplotlib.


**Basics.** Conda has a number of tools for managing our Python installation.  Try each of these commands (from the command line -- _not_ inside Ipython or spyder) and see what happens:

```
conda info
conda help
```

The first one tells us the version of Conda we have.  It knows whether we installed the Windows, Mac, or Linux versions, and tells us where Anaconda is installed on our computer.

The second line gives us a list of Conda commands.  We'll focus on `update` and `install`, but first let's see what we've got installed.


**Exercise.** Enter `conda list`.  How many packages do you have installed?  Verify that Pandas and Matplotlib are among them.  What versions do you have?

**Exercise.** Go to the [Anaconda package list](http://docs.continuum.io/anaconda/pkg-docs) and verify that it contains Seaborn.  Use `conda list` to see if we already installed it.  (Probably not, but it's worth checking.)


**Updating.**  The next step is to update our Python installation.  Updating with Conda is simpler than installing Anaconda again, and less likely to lead to trouble.  First we update Conda:

```
conda update conda
```

This checks to see how our installation compares to the current version.  If we're up to date, it will respond:  `All requested packages already installed.`  If not, we get a long list of packages and the question:  `Proceed ([y]/n)?` (Or just hit return and yes will be assumed.)

Next we update Anaconda:

```
conda update anaconda
```

If we're up to date, we get the same response as before.  If not, it will ask us to type `y` (yes) or `n` (no) to update our version.  Type `y` to update.  This can take a while, you might want to get a cold drink while you're waiting.


**Exercise.** Update Conda and Anaconda on your computer.


**Installing new packages.**  Next up:  installing a new packages.  If we want to install a package, and it's part of the [Anaconda distribution](https://docs.continuum.io/anaconda/pkg-docs), we install it with

```
conda install [package]
```

Here `[package]` stands for whatever package we have in mind.

**Exercise.** Install the graphics package Seaborn with

```
conda install seaborn
```

**Exercise.** Install the data input package `pandas-datareader`. This will be needed in the next chapter, so do not skip this exercise!

### Pip

Pip is the traditional Python package management tool.  While Conda accesses packages included in Anaconda, Pip accesses a larger number of packages stored in the **Python Package Index**, commonly referred to as PyPI or the [Cheese Shop](https://en.wikipedia.org/wiki/Cheese_Shop_sketch).

Pip works pretty much the same way Conda works.  We type things like this at the command line prompt:

```
pip help
pip list
pip install [package]
```

(This should remind you of what we just did with `conda`?)  We won't speak more about it, but if you use a package that's not in Anaconda, this is the fallback.

**Exercise.** Use pip to install the `plotly` package. It is another package for creating plots in Python and we will use it later in the course.


<!--
## Quandl

Handy access to lots of economic and financial data...

## Seaborn

A terrific interface for Matplotlib...

## tqdm

Progress bar for data loads...


## Pyopendata

https://pypi.python.org/pypi/pyopendata/0.0.2

Use to get OECD data?


## Flappy bird

https://www.youtube.com/watch?v=h2Uhla6nLDU
https://github.com/Max00355/FlappyBird/blob/master/flappybird.py
-->

### Resources

The documentation has way more than we want or need, but the [Conda cheatsheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf) isn't bad.

<!--

http://people.duke.edu/~ccc14/sta-663/IntroductionToPythonSolutions.html#keeping-the-anaconda-distribution-up-to-date

-->
