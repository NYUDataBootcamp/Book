# ??Visualizing principles


---
**Overview.**

**Python tools.**

**Buzzwords.**

**Applications.**

**Code.** Link.

---


Seaborn

heatmaps

animations


OLD FOLLOWS


http://blog.dominodatalab.com/lesser-known-ways-of-using-notebooks/


**Pro tips.**

* Close running notebooks.  go to the run tab and shut down other notebooks.  If none, you're ok.

* List keyboard shortcuts.  Type h.

* %matplotlib inline


## IPython Magics

%%time

##  Matplotlib 1:  the pyplot module

Functions and methods...


**Add data source text at bottom**


## Object-oriented matplotlib




## Dataframe methods


Special methods for dataframes...



## Examples

http://fivethirtyeight.com/datalab/the-extreme-economic-outlier-that-is-greece-in-7-charts/

Chetty 100 x 100 heatmap?
http://www.equality-of-opportunity.org/images/online_data_tables.xls

## Style sheets

```python
import matplotlib.pyplot as plt

# http://matplotlib.org/users/style_sheets.html
plt.style.use('ggplot')
plt.style.reload_library()  # does this reset default?
```


xkcd-style graphs

great example of documenting code:  https://jakevdp.github.io/blog/2012/10/07/xkcd-style-plots-in-matplotlib/
http://jakevdp.github.io/blog/2013/07/10/XKCD-plots-in-matplotlib/

http://matplotlib.org/examples/showcase/xkcd.html

fonts:  http://stackoverflow.com/questions/19663986/getting-xkcd-plots-using-matplotlib

Revert to defaults:  http://stackoverflow.com/questions/26413185/how-to-recover-matplotlib-defaults-after-setting-stylesheet

import matplotlib as mpl
mpl.rcParams.update(mpl.rcParamsDefault)

Also saw this:   plt.rcdefaults()

Diff in IPython...


## Links

Viz of the Day
Tableau
Viz Wiz

Graphic Detail*


Heatmaps:  http://stackoverflow.com/questions/14391959/heatmap-in-matplotlib-with-pcolor


## Resources

IPython

* http://blog.endpoint.com/2015/06/ipython-tips-and-tricks.html

* https://github.com/rhiever/ipython-notebook-workshop

Matplotlib

* Matplotlib's [Pyplot tutorial](http://matplotlib.org/users/pyplot_tutorial.html) is excellent.

* Matplotlib's [gallery of examples](http://matplotlib.org/gallery.html) is also a great starting point.  Find an example you like, download the code, and adapt it to your needs.

* Another gallery:  https://www.getdatajoy.com/examples/python-plots

* Rougier, Mueller, and Varoquaux's [SciPy lecture notes](https://scipy-lectures.github.io/intro/matplotlib/matplotlib.html) are also quite good.  It's aimed at scientists, so the examples tend to be mathematical.  Their [cookbook](http://wiki.scipy.org/Cookbook/Matplotlib) has a good collection of samples.

* http://nbviewer.ipython.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb

* Sargent and Stachurski's [Quantitative Economics](http://quant-econ.net/) has a good overview of Matplotlib, but we find it a little terse.

* [Practical business Python](http://pbpython.com/visualization-tools-1.html) is a terrific blog.  This post concerns Python visualization packages.  He likes Seaborn.

https://github.com/rasbt/matplotlib-gallery

Check this out:  Benjamin Root and Joe Kington, SciPy 2015.
https://youtu.be/MKucn8NtVeI
https://github.com/WeatherGod/AnatomyOfMatplotlib

Colormap:  https://www.youtube.com/watch?v=xAoljeRJ3lU .  Sort of interesting, moderately technical, short.

http://nbviewer.ipython.org/gist/msund/11349097
https://www.reddit.com/r/Python/comments/2cfulw/indepth_matplotlib_tutorials_beginner_to_advanced/
http://pythonprogramming.net/matplotlib-graphing-series/


https://conference.scipy.org/scipy2013/tutorial_detail.php?id=103

Jake:  https://vimeo.com/53057312
http://jakevdp.github.io/mpl_tutorial/

Tufte interview:  http://adage.com/article/adagestat/edward-tufte-adagestat-q-a/230884/


http://civilstat.com/2015/10/statistical-graphics-and-visualization-course-materials/
http://biostat.mc.vanderbilt.edu/wiki/pub/Main/RafeDonahue/fscipdpfcbg_currentversion.pdf