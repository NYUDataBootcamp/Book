# Updating Python:  Conda and Pip


---
**Overview.**  We describe tools used to update and install Python packages.

**Python tools.**  Conda, Pip.

**Buzzwords.**  Command line.

**Applications.**  Seaborn, Bokeh, pandas-datareader.

---


**Warning:  This is a little terse, but we think it does the trick.**

Python has some handy tools for installing and updating the core language and its packages.  We start with **conda**, the tool used to update the components of the Anaconda distribution, then move on to the traditional Python tool, **pip** ("pip installs packages").

As usual, the idea is to get things started.  We provide links to more extensive documentation at the end.


## The command line

These tools run on the **command line**, the old-school approach to computing that predates the graphical interfaces we use today (Mac OS, Windows, etc).  Picture the computer screens in "[War Games](http://pc-museum.com/046-imsai8080/wargames.htm)."  Many of the graphical interfaces used in the computing world run things on the command line behind the scenes, so it's often better to go straight to the source and run things on the command line ourselves.

Here's how we access the command line:

* In Windows.  Press the Windows key or the Windows icon.  A textbook will pop up.  Type "cmd" and enter.  You should see a open window with a prompt that looks like this:

     ```
     bla bla bla
     C:\Users\username>
     ```

     We can -- and will -- enter commands at the prompt.

* In Mac OS.  Click the magnifying glass at the top right and enter "terminal".  You should see something like this:

     ```
     bla bla bla
     MacBook-Pro:~ Usename:
     ```

     That serves the same purpose.


## Conda

Conda is the Anaconda tool.  We use the Anaconda distribution of Python, which we think is the most user-friendly version out there.  It comes with a variety of packages installed, including our favorites:  Pandas and Matplotlib.


**Basics.** Conda has a number of tools for managing our Python installation.  Try each of these commands and see what happens:

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

**Exercise.** Install the data input package `pandas-datareader`.


## Pip

Pip is the traditional Python package management tool.  While Conda accesses packages included in Anaconda, Pip accesses a larger number of packages stored in the **Python Package Index**, commonly referred to as PyPI or the Cheese Shop.

Pip works pretty much the same way Conda works.  We type things like this at the command line prompt:

```
pip help
pip list
pip install [package]
```

(Look familiar?)  We won't speak more about it, but if you use a package that's not in Anaconda, this is the fallback.


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

## Resources

The documentation has way more than we want or need, but the [Conda cheatsheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf) isn't bad.

<!--

http://people.duke.edu/~ccc14/sta-663/IntroductionToPythonSolutions.html#keeping-the-anaconda-distribution-up-to-date

-->
