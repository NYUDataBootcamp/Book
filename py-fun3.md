# Python fundamentals 3


---
**Overview.**   Advanced core Python.

**Python tools.**  iterables, generators, classes...

---


## Special Python functions

This is all mtyn and we don't plan to use any of it.  We include it because we got carried away.

We can define one-line **lambda functions.** in a streamlined way.  To compute the ever-popular square of a number, we can define the function

```python
square = lambda x:  x**2
```

We can now compute the square of 8 with `square(8)`.

There are three functions that do implicit loops of different kinds:

* **map.** The statement `map(function, list)` applies a function to all the elements of a list or similar object, producing another list of the same length.  An example:
```python
anylist = [2, 'Steelers', [1,2,3]]
m = map(type, anylist)
types = list(m)
```
The last line is needed because `map` produces a "map object," which isn't all that helpful on its own.  So we converted it to a list.

* **reduce.** The statement `reduce(function, list)` applies a function to the elements of a list and produces a single value.  The idea is that the calculations are connected. For example, we could compute a sum one element at a time:
```python
from functools import *
numlist = [4, -2, 5]
sum = reduce(lambda x,y: x+y, numlist)
```
The difference here is that the computations cannot be done separately, they're all connected.

* **filter.**  Here we apply a logical condition to each element of a list or similar object and keep those for which the condition is true.  Two examples:
```python
numlist = [4, -2, 5]
f = filter(lambda x:  x >= 0, numlist)
newlist = list(f)
anylist = [2, 'Steelers', [1,2,3]]
f = filter(lambda x: type(x) == str, anylist)
newlist = list(f)
```
The first one has the answer `newlist = [4, 5]`, the second `newlist = ['Steelers']`.  Can you see why?

[?? talk about each one as an implicit loop?]

Some of us find this kind of syntax obscure and do our best to avoid it.  But similar ideas show up in lots of places.

See also <br>
http://people.duke.edu/~ccc14/sta-663/FunctionsSolutions.html#higher-order-functions <br>
http://people.duke.edu/~ccc14/sta-663/FunctionsSolutions.html#anonymous-functions


## Classes, iterators, generators, ...

Maybe some time.


## Resources

http://blog.lerner.co.il/pythons-objects-and-classes-a-visual-guide/
http://blog.lerner.co.il/want-to-understand-pythons-comprehensions-think-like-an-accountant/
http://blog.lerner.co.il/quick-introduction-implementing-python-iterators/


