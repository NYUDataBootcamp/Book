# Plotly

---
**Overview.**  We introduce and apply a new and exciting graphics package plotly.  We show how we can leverage our knowledge of Matplotlib to jumpstart our usage of plotly. We then show how to access some of plotly's unique features to do things that are difficult or impossible with our knowledge of matplotilb.

**Python tools.**  IPython notebooks in Jupyter. JSON. Graphing with plotly.

**Buzzwords.** Data visualization, interactive graphics, maps

**Applications.**  TODO

**Code.** [Link](https://github.com/NYUDataBootcamp/Materials/blob/master/Code/notebooks/bootcamp_plotly.ipynb).

---

There are many ways to create graphics with Python. We've already become
familiar with the de-facto standard graphics library Matplotlib. We've also
seen that seaborn provides a high-level interface for drawing attractive
statistical graphics. In this chapter we will learn about an exciting new
charting library plotly.

## Reminders

* Packages.  Collections of tools that extend Python's capabilities. We add them with `import` statements.
* `conda` and `pip`: package managers for python. Install new packages using `conda install package_name` or `pip3 install package name`.

We will need to have the plotly python package installed. To do this enter the
following from the command line (command prompt on windows, terminal on mac):

```shell
pip3 install plotly --upgrade
```

Once you've done that, come back to this notebook and run the following cell to
make sure plotly is installed properly.

```python
import sys                             # system module
import pandas as pd                    # data package
import matplotlib.pyplot as plt        # graphics module
import datetime as dt                  # date and time module
import numpy as np                     # foundation for Pandas
import plotly as py                    # plotly

%matplotlib inline

# check versions (overkill, but why not?)
print('Python version:', sys.version)
print('Pandas version: ', pd.__version__)
print('Plotly version: ', py.__version__)
print('Today: ', dt.date.today())
```

## Background

Plotly is a javascript based plotting library. Plotly leverages industry grade
javascript technologies to provide great flexibility and good performance.
Being a javascript library, plotly graphics are meant to be viewed in a
web-browser. The good news is that we can embed our interactive plots in any
website: Jupyter notebooks, blog posts, etc. The *great* news is that we don't
have to write any javascript ourselves!

The plotly project was started about four years ago. Over that time, plotly has
transitioned between three phases:

1. Online only mode: plotly started as a web service where you uploaded your
data and constructed plots on their website.
2. Online plotting mode: the next phase was to allow you to build plots from
your favorite programming language (Python!), but the plots were actually
created on their servers and you were given a link to view the plot on their
website.
3. Offline mode: You can now construct plotly graphics 100% offline. While all
three modes still exist, we will use the purely offline mode in our notes.

## Matplotlylib

As a warmup, let's utilize our expertise of Matplotlib to quickly generate

## Plotly API

Let's now consider how to use plotly's own API to construct plots instead of
building the graphics through matplotlib.

Plotly has a purely **declarative** API. This means that we describe all the
features we want in our figure at once, without worrying about which functions
to call in what order.
