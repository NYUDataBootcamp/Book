# Pandas 3: Shaping data

---
**Overview.**

**Python tools.**

**Buzzwords.**

**Applications.**

**Code.** Link.

---

FOLDED INTO PREVIOUS CHAPTER

## Reminders

DataFrames:  index, columns

Want operator

Chipotle <br>
Yahoo finance:  Ju's example, reshape <br>
World Bank data <br>



## Setting the index



## Multi-indexes

* WEO
* Yahoo finance


## Stacking and unstacking


stack... (Rhodes 1:34)

unstack:  Brandon Rhodes at 2:00



## Pivot





## Panel data

Diff structure for multi-index...

Suggestion:  use the `to_frame` method to convert to a multi-indexed dataframe


Here's an example from a student, who was downloading stock prices. Here we download daily stock prices for Apple and Google.



<!--
We'll talk more about packages later, but for now just put these lines above...

```python
import pandas as pd
```

https://realpython.com/blog/python/working-with-large-excel-files-in-pandas/


Methods to cover

describe
value_counts
set_index  --- and  .sort_index() to speed up selection
also multiindexes:  df.set_index(['var1', 'var2'])
reset_index -- puts index into varlist

df.loc['var1'].loc['var2']
df.loc['var1', entry]

groupby -- sorts automatically
size, sum, mean, max, min

data types for variables (info?)

## Missing values


## Stack and unstack...


unstack... (Rhodes 1:34)

unstack:  Brandon Rhodes at 2:00
 

## Pivot tables

https://en.wikipedia.org/wiki/Pivot_table

Rhodes:  You can all of it and more with set_index, sort_index, and unstack.  2:10m



## Merging dataframes

merge:  Brandon Rhodes at 2:10

Evidently Pandas is smart...


## Examples

Auto safety:  http://www.nhtsa.gov/NCSA

-->


## References

Brandon Rhodes.  This is great.
https://youtu.be/5JnMutdy6Fw
https://github.com/brandon-rhodes/pycon-pandas-tutorial/


<!--
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