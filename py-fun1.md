# Python fundamentals 1

---
**Overview.**  Time to start programming!  We work our way through some of the essentials of Python's core language.  We will do this within a Jupyter Notebook and along the way become familiar Markdown other properties of the notebook environment.  Part 1 of 2.

**Python tools.**  Syntax, Jupyter, calculations, assignments, strings, lists, built-in functions, objects, methods, tab completion, object inspector.

**Buzzwords.** Isn't that enough?

**Trigger warning.**  Technical content, cannot be mastered without effort.

---

We're now ready to explore the rudiments of Python.  We're going to **jump right in** to the deep end of the pool.  For a couple weeks, you may feel like you've been dropped in a foreign country where you don't speak the language.  You'll hear terms like "strings", "floats", "objects", "methods", and "tab completion".  Some of these are words you know, but even so, they tend not to mean what you think they mean.  (Insert [Princess Bride](http://www.imdb.com/title/tt0093779/quotes?item=qt0482717) joke.)

Don't panic, it's just jargon.  If you put some effort into this over the next 2-4 weeks, you'll be fine.  And ask questions.  Really. **Ask lots of questions.**

The challenge and beauty of writing computer programs is that we need to be precise.  If we mistype anything, the program won't work.  Or it might seem to work, but the output won't be what we expect.  In formal terms, the **syntax** -- the set of rules governing the language -- is less flexible than natural language (English, for example).

We mix Python concepts with an introduction to **Jupyter** which also comes with its own features (outside of the Python ecosystem). A key feature of Jupyter notebooks is the ability to mix text with code. The text component is **Markdown** which is a text fromating language (you provide the text, it makes the style) that can easily be converted into HTML. May be **mtwn** but its ok!

## Jupyter essentials.

**Opening Jupyter** Let's remind ourselves how to do this...

* Open your terminal (command prompt on Windows)

* Type `jupyter notebook` and press enter.  This will open a tab in your browser with the word Jupyter at the top and your computer's directory structure below it.

* In the browser tab, navigate to your `Data_Bootcamp` directory/folder.

* Click on the New button in the upper right and choose `Python 3` (it may also refer to this as `Python[Root]`.

In your browser, you should have an empty notebook with the word Jupyter at the top.  Below it is a **menubar** with the words File, Edit, View, Cell, Kernel, and Help.  Below that is a **toolbar** with various buttons.  You can see all of these components here:

![Jupyter environment](figs/jupyter_notebook.png "Jupyter")

If you have a few minutes, click on Help in the menubar and choose User Interface Tour.

Let's put some of these tools to work:

* Change the notebook name.  Click on the name (`Untitled` if we just created a new notebook) to the right of the word Jupyter at the top. A textbox should open up.  Use it to change the name to `bootcamp_sandbox`.

* Toolbar buttons.  Let your mouse hover over one of them to see what it does.

* Add a cell.  Click on the `+` in the toolbar to create a new cell.  Choose Code in the toolbar's dropdown menu.  Type this code in the cell:

  ```python
  import datetime as dt
  print('Welcome to Data Bootcamp!')
  print('Today is: ', dt.date.today())
  ```

  Now click on Cell in the menubar and choose Run cell.  You should see the welcome message and today's date below the code.

* Add another cell.  Click on the `+` to create another cell and choose Markdown in the toolbar's dropdown menu. Markdown is text; more on it shortly.  Type this in the cell:

  ```
  Your name
  Data Bootcamp sandbox for playing around with Jupyter notebooks
  ```

  Run this cell as well.

You get the idea.  To get a sense of what's possible, take a look at these two notebooks [1](https://github.com/NYUDataBootcamp/Materials/blob/master/Code/notebooks/bootcamp_test.ipynb) [2](http://nbviewer.ipython.org/github/justmarkham/DAT4/blob/master/notebooks/08_linear_regression.ipynb).

In addition to the buttons near the top of your notebook, there are also **keyboard shortcuts** for all these commands. We'll tell you about them along the way. Once we got used to them, we found that the keyboard shortcuts are an easier and more efficient way to do what we need. Here are the ones I find most useful:

* The command for creating a new cell is to press escape to be in *command mode* and then press `a` to insert a new cell above the current one and `b` to insert a new cell below the current cell. How do I know the cell is in command mode? First, there should be a slim vertical bar to the left of the cell which should be blue when in command mode, green otherwise. Second, you won't see a cursor!

* To change the type of cell (Markdown or Python), in *command mode* you type `y` for a python cell and `m` for a markdown cell.

* To run a cell, just hit `shift` and `enter` at the same time.  

**Markdown essentials.**  Markdown is a simplified version of html ("hypertext markup language"), the language used to construct basic websites.  html was a great thing in 1995, but now that the excitement has worn off we find it painful.  Markdown, however, has a zen-like simplicity and beauty.  Here are some things we can do with it:

* Headings.  Large bold headings are marked by hashes (`#`).  One hash for first level (very large), two for second level (a little smaller), three for third level (smaller still), four for fourth (the smallest).  Try these in a Markdown cell to see how they look:

   ```
   # Data Bootcamp sandbox
   ## Data Bootcamp sandbox
   ### Data Bootcamp sandbox
   ```

  Be sure to run the cell when you're done (`shift enter`).

* Bold and italics.  If we put a word or phrase between double asterisks, it's displayed in bold.  Thus `**bold**` displays as **bold**.  If we use single asterisks, we get italics:  `*italics*` displays as *italics*.

* Bullet lists.  If we want a list of items marked by bullets, we start with a blank line and mark each item with an asterisk on a new line:

  ```markdown
  * something
  * something else
  ```

  Try it and see.

* Links.   We construct a link with the text in square brackets and the url in parentheses immediately afterwards.  Try this one:

  ```
  [Data Bootcamp course](http://nyu.data-bootcamp.com/)
  ```

We can find more information about Markdown under Help.  Or use your Google fu.  We like the [Daring Fireball](https://daringfireball.net/projects/markdown/) description.

Markdown is ubiquitous.  This book, for example, is written in Markdown.  Look [here](https://github.com/NYUDataBootcamp/Book) for a list of chapter files.  Click on one to see how it displays.  Click on the Raw button at the top to see the Markdown file that produced it.

**Exercise.**  Ask questions if you find any of these steps mysterious:
* Close Jupyter.
* Start Jupyter.
* In Jupyter, open an new Ipython notebook within your `Data_Bootcamp` directory/folder, point to the code cell, the name of the notebook, and the help button.
* Save the file  `bootcamp_class_pyfun1` in your   This file will serve as your notes for this class.
* Create a description cell in Markdown at the top of your notebook.  It should include your name and a description of what you're doing in the notebook.  For example: "Mike Waugh's first notebook for Python fundamentals 1" and a date.

## The logic of Python programs

In a spreadsheet program such as Excel, we can connect cells to other cells.  Then when we change one cell, any other cells connected to it update automatically.

Most computer programs, including Python programs, don't work that way.  They run one line at a time, starting at the top of the program and working through the list of instructions until they reach the end or stop for some other reason.  A program is just a detailed list of things we want the computer to do.

Most of the programs in this course have the structure:

* Input data.
* Manipulate the data until it's in the form we want.
* Produce some graphics that summarize the data in a compelling way.

Each of these bullet points is typically associated with a number of lines of code, possibly a large number, but that's the general idea.


## Calculations

We'll do lots of numerical calculations.  That's mostly what managing data is about: adding things up, dividing one thing by another, and so on.

To see how calculations work in Python, type these expressions their **own individual cell**:

```python
2*3
2 * 3
2/3
2^3
2**3
log(3)
```

Type each one into the console, hit return, and look to see what happens.  The first one multiplies 2 times 3, and (hopefully) gives us 6 as the answer.  The input and output look like this in the console:

```
In [1]: 2*3
Out[1]: 6
```

The first line is our input, we typed it.  The number in brackets `[1]` is a line number.  We don't type it, it's there in the console to begin with.  As we proceed the number [1] increases to [2], [3], and so on.  The second line --- the one that starts `Out[1]` --- is the response or output Python produces.

The second calculation, `2 * 3`, does the same thing.  The spaces around the * don't change the output.  As a general rule, we can put spaces wherever we think they make the code more readable --- In fact, Python's [style guide](https://www.python.org/dev/peps/pep-0008/) encourages you to [use white space](https://www.python.org/dev/peps/pep-0008/#whitespace-in-expressions-and-statements) in a way that makes your code readable.

The third calculation is division.  The input and output are

```
In [3]: 2/3
Out[3]: 0.6666666666666666
```

The fourth calculation, `2^3`, gives us

```
In [4]: 2^3
Out[4]: 1
```

Hmmmm.  What just happened?  We expected the answer to be 8 (2 to the power 3), but evidently it's not.  The short answer is that the hat symbol `^` doesn't do exponents in Python, as it does in Excel.  It does something else, which we won't go into.

That makes this is a good time to practice our **Google fu**:

**Exercise.** Use Google to search for "python exponents."  Use what you find to compute 2 to the power 3.  (Don't look below, that's cheating.)

We should find, after wading through the links, that exponents in Python are done this way:

```
In [5]: 2**3
Out[5]: 8
```

**Exercise.** What does the calculation `2 ** 3` produce?

Our last calculation is the log function.  Entering `log(3)` generates the message:  `NameError: name 'log' is not defined`.   This is an example of a **syntax error**:  we have used language that Python doesn't understand.  Here the message is pretty clear:  it doesn't know what `log` means.  In other cases, the error message may be more mysterious.  We can use functions like `log` and `sqrt` in Python, just as we do in Excel, but we need to import them specially.  (And we will, but not yet.)

**Exercise.**  What happens if you try to calculate the square root of 2 with `sqrt(2)`, as you would in Excel?  How would you do it (You don't need to import it -- Hint: square root is a power)?


## Assigning values to variables

Or maybe we should use scare quotes:  "Assigning" "values" to "variables."

We'll start with examples and explain what they do.  Type these two lines into a code cell.

```python
x = 2
y = 3
```

In each of these lines:

* The thing on the left is called a **variable**. In the first line, `x` is the variable.  In the second, `y` is the variable.
* The thing on the right is a **value**.  In the first line, `2` is the value.  In the second, `3` is the value.
* The equals sign `=` **assigns** the value on the right to the variable on the left.  Thus the first line assigns the value `2` to the variable `x`.  The second assigns the value `3` to the variable `y`.

We call statements like these **assignments**:  We assign a value to a variable.

We can see the results of these assignments by checking the contents of the variables `x` and `y`.  In a code cell, typing a variable and hitting return gives us its value. If we type `x` and `y`, one at a time, we get

```
In [7]: x
Out[7]: 2
In [8]: y
Out[8]: 3
```

So we see that the variables now contain the values we assigned them.

Variables are handy ways of storing values.  We can use them in future calculations simply by using their names, just as we would use a cell address in Excel.  Here's an example.  Type this into a code cell:

```python
z = x/y
```

If we type `z` in another code cell and then evaluate it, we get

```
In [9]: z
Out[9]: 0.666666666
```

What's going on here?  We take `x` (which now has a value of 2) and divide it by `y` (which now has the value of 3) and assigns it to the variable `z`.  The result is a computer's version of two-thirds.

**Exercise.** Type `w = 7` in a cell.  In the same cell, next line below, type `w = w + 2`. In the next line below type `w` (so we can see the output). What does this code do?  Why is this not a violation of basic mathematics?

**Exercise.** In another code cell type `w = w + 2` and then `w` below it (again so we can see the output). Evaluate this cell once. Do it again. Do it again. What is going on here?

**Exercise.**  Suppose we borrow 200 for one year at an interest rate of 5 percent.  If we pay interest plus principal at the end of the year, what is our total payment?  Compute this using the variables `principal = 200` and `i = 0.05`.

**Exercise.** Real GDP in the US (the total value of things produced) was 15.58 trillion in 2013 and 15.96 trillion in 2014.  What was the growth rate?  Express it as an annual percentage.

**Exercise (challenging).**  Suppose we have two variables, `x` and `y`.  How would you switch their values, so that `x` takes on `y`'s value and `y` takes on `x`'s?

**Exercise (challenging).**  Type `x = 6` in a cell.  We've reassigned `x` so that its value is now 6, not 2. If we type and submit `z`, we see

```
In [10]: z
Out[10]: .6666666666
```

But wait, if `z` is supposed to be `x/y`, and `x` now equals 6, then shouldn't `z` be 2? What do you think is going on?


## Displaying results with the `print()` function

We saw that when we performed a calculation, such as `z = x/y`, we had to ask to see the result.  The `print()` function gives us another way to do that.  If we type `print(z)`  we get

```
In [11]: print(z)
0.6666666666666666
```

Evidently this displays the value of `z`, namely `0.6666666666666666`.  We will use print statements a lot to track the progress of our code. We need to do this because Python -- and all other programming languages -- will not report back the results of what we ask it to compute unless we tell it to do so.

The print function displays whatever we include in parentheses after the word print:  for example, `print(x)`.  If we want to print more than one thing, we separate them with commas; for example, `print(x, y)`. That's the **general structure of functions** in Python:  a function name (in this case `print`) followed by inputs ("arguments" or "parameters") in parentheses that are separated by commas.  We usually refer to the `print()` function, with explicit parentheses, to remind ourselves that it requires input of some kind.

So if we want to verify the calculation of `z`, we can type `print(z)` in a code cell.  If we want to print all the calculations from the previous section, we can type `print(x, y, z)`:

```
In [12]: print(x, y, z)
2 3 0.6666666666666666
```

By default, the output is separated by spaces.


We'll use more complicated print statements than this, which we'll explain as we go.  But if you see something you don't recognize, remember to **ask questions**.


## Getting help in Jupyter

If you want to know more about a function, the main approach is to simply type the function name and then a question mark after it in a code cell and then evaluate it. This works for any function, but using print as our examples we can:

* Type `print?` in the code cell and hit `shift` and `enter`

The same approaches work for other functions.  We use them both a lot.  If they fail, either because there's no help or the help is incomprehensible, we fall back on Google fu.

**Exercise.**  Run this statement:  `print(x, y, z, sep='|')`.  Use the output and Jupyter's help to explain what the `sep` argument does.


## Strings

We often work with non-numerical data, collections of characters that might include letters, numbers, or other symbols.  Such things show up in a lot in data work, as variable names (GDP, income, volatility) and even as data (country or customer names, for example).  We refer these as **strings**.  This doesn't mean what we think it means.  No, not the stuff we tie up packages with, but a "string" of characters like letters or numbers.  It's one of many mysterious uses of ordinary words we'll run across as we learn to code.  For more on this one, see [here](http://stackoverflow.com/questions/880195/the-history-behind-the-definition-of-a-string).

We create strings by putting characters between quotation marks: 'Chase', "Spencer", 'Sarah', "apple", and even "12" are all strings.  Single and double quotes both work.

The last example is a confusing one, because it looks like a number.  It's not.  The number `"12"` is between quotes, so it's a string.  If we try to use it as a number, it doesn't work.  Try, for example, `'12'/3`.  This generates the error:  `TypeError: unsupported operand type(s) for /: 'str' and 'int'`.  What this means is that we tried to divide a string (`"12"`) by an integer (`3`).  That's no different to Python than trying to divide your name by three, it can't make sense of it.

We repeat:  **a string is a collection of characters between quotes**. The characters can be pretty much anything. Therefore `12` is a number (no quotes), but `"12"` is a string.

Here are some other examples, which we assign to variable names for later use. Type them into its **own individual cell**:

```python
a = 'some'
b = 'thing'
c = a + b
d = '12.34'
```

What do you see?  The first two are probably obvious:  We assign the characters in single quotes on the right to the variables on the left.

The third line is something new:  We add the string `some` to the string `thing`.  What would you expect to get?  Try `print(c)` to find out.  That gives us the answer: `c = 'something'`.  We've simply stitched the two strings together, one after the other. **WOW...** this is awesome.

Strings also allow us to produce better-looking output.  In the previous section, for example, we can change the statement `print(z)` to `print('The value of z is ', z)`.  The first argument (or input), `'The value of z is '`, is a string.  The second argument, `z`, is a variable.  Together they produce the output `The value of z is  0.6666666666666666`, which is clearer than the number `0.6666666666666666` on its own.  Or we could spread this over two lines:

```python
message = 'The value of z is '
print(message, z)
```

Here we've taken the components of the previous print statement and expressed them in two statements to make it more readable.  (You might ask yourself:  Which do you prefer?  Why?)

**Exercise.** What is a string?  How would you explain it to a friend?

**Exercise.** What happens if we run the statement:  `'Chase'/2`?  Why?

**Exercise.** This one's a little harder.  Assign your first name as a string to the variable `firstname` and your last name to the variable `lastname`.  Use them to construct a new variable equal to your first name, a space, then your last name.  *Hint:*  Think about how you would express a space as a string.

**Exercise.** Set `s = 'string'`.  What is `s + s`?  `2*s`?  `s*2`?  What is the logic here?

<!--
u and r in string literals
https://stackoverflow.com/questions/2081640/what-exactly-do-u-and-r-string-flags-do-in-python-and-what-are-raw-string-l
https://en.wikipedia.org/wiki/String_literal
-->


## Structuring code within Jupyter

Lets take a quick step back and discuss how to **use** Jupyter to create effective, readable code. Often we are writing much longer programs. In this case it would be silly to have every single cell be composed of just one line. Why? Lots of reasons, but the most important reasons is that that reading the code AND understanding it's context within the whole program would be very hard to do. **And readable code is something that we should aspire to (see the links in the next section).**

OK. What should I do? Use a code cell for a certain task. For example, one code cell is dedicated to reading in the data. Another code cell performs one manipulation of the data (which could take multiple lines of code), another code cell performs a different manipulation, and then another is dedicated to plotting a figure. So each code cell is accomplishing a specific task at hand.

Why not put everything in one code cell? Again, this is problematic regarding readability. Second, chopping up the code into different cells is good for debugging. For example, you may have aspects of your code that works, but other parts are having problems (it will happen...). So rather than running the whole program over and over again to debug only a subset, you have that subset of code in its own cell and then work on that on its own.

Let's give it a try.  Type these commands into **one** code cell:

```python
a = 'some'
b = 'thing'
c = a + b
print('c =', c)
```
When we run the code, we see that the first three lines produce no output.  The last one produces the output `c = something`. What we have now is one code cell performing one distinct task.  

## Using Markdown to facilitate readability

One of the nice features of Jupyter is that it can mix nicely formatted text via Markdown with code. This allows you to describe, at a high-level the steps that your analysis is walking through. The "high-level" aspect of this is nice in that you can structure your notebook where, say your Manager, can follow your steps without having to delve deep into the details of the code. Moreover, this allows us to "tell the story" when working with data.

For example, in the cell above the code discussed above, you could insert a cell saying something to the effect:
```Markdown
# Creating a word by addition
Here is an example where I am using the addition function on strings to create the word something
```

**Exercise.** Do this. Remind yourself how to create a markdown cell and insert the markdown code above the "something" code cell.

## Add comments to your code

We also want to mechanically explain what individual lines of code our doing. One of the rules of good code is that **we explain what we've done---in the code**.  Think about this aspect as writing and explaining code that one of our classmates can understand without help. These explanations are referred to as comments.

Add a comment with the hash character (#).  Anything in a line after a hash is a comment, meaning it's ignored by Python.  Here are some examples:

```python
# everything that appears after this symbol (in the same line) is a comment!
# comments help PEOPLE understand the code, but PYTHON ignores them!
# we're going to add 4 and 5
4 + 5           # here we're doing it
print(4+5)      # here we're printing it
```

We often put comments like this in our code.  Not quite this basic, but close. One of the unwritten "laws of nature" in programming is that code is read much more often than it is written. See these links...they're awesome:
[1](http://docs.python-guide.org/en/latest/writing/style/) [2](https://blogs.msdn.microsoft.com/oldnewthing/20070406-00/?p=27343) [3](https://blog.codinghorror.com/when-understanding-means-rewriting/).

Writing informative comments will not only lead to others thanking you for saving them time, but you will find that you thank yourself very frequently.

**Exercise moving forward.** Practice writing comments **all the time**. Whenever you learn something new, write a comment explaining it in your code. It feels tedious, but the best coders always explain their work. It's a good habit to develop.


## Single, double, and triple quotes

We typically define strings by putting characters between single quotes, as in `a = 'some'`.  That will be our standard practice, but **Python treats single and double quotes the same**.  We could have typed `a = "some"` (that is, with double quotes) with the same effect.  The main reason for using single quotes is laziness: we don't have to hit the shift key.  We're not ones to disparage laziness, but the point is that there's no difference between the two.

There are, however, some special cases where double quotes come in handy.  On occasion, we use double quotes if the string includes a single quote:

```python
f = "I don't believe it"
print(f)
```

The output of the print statement is `I don't believe it`, which includes a single quote as an apostrophe. This doesn't come up very often, in our experience, but there it is just in case.


Triple quotes are similar, but they can be used to define strings that go over several lines:

```python
longstring = """
Four score and seven years ago
Our fathers brought forth. """
print(longstring)
```

This produces the output

```python

Four score and seven years ago
Our fathers brought forth ...
```

The blank line comes from the empty space to the right of the first triple quote.  And yes: we can make triple quotes from single quotes -- and this is more than we need.

We often put long quotes like this at the top of our programs.  Officially they're strings, but unofficially they're comments.  Here's an example from the start of our test program:

```python
"""
Data Bootcamp test program checks to see that we're running Python 3.
Written by Dave Backus, March 2015
Created with Python 3.4
"""
```

**Exercise.** Put a comment like this at the top of your program.


**Exercise.** In the `Four score etc` code, replace the triple double quotes with triple single quotes. What happens?


**Exercise.** Fix this code:

```python
bad_string = 'Sarah's code'
```

**Exercise.** Which of these are strings? Which are not?

```python
apple
"orange"
'lemon84'
"1"
string
4
15.6
'32.5'
```


## Lists

<!--
Lists are one of the fundamental Python **data structures**, a term that means a specific organization of data.
-->

A Python list is what it sounds like:  an ordered collection of items.  The items can be lots of things:  numbers, strings, variables, or even other lists.

**Creating lists.** We create lists by putting **square brackets around a collection of items** separated by commas.  Here are some examples. Type each line of code into a code cell and run them.

```python
numberlist = [1, 5, -3]
stringlist = ['hi', 'hello', 'hey']
```

These are, of course, assignments:  the lists on the right are assigned to the variables on the left.

We can also make lists of variables:

```python
a = 'some'
b = 'thing'
c = a + b
variablelist = [a, b, c]
```

Or we can combine variables, numbers, and strings:

```python
randomlist = [1, "hello", a]
```

**Combining lists.** We can combine lists (literally) by adding them.  The statement `biglist = numberlist + stringlist` produces a list containing all the elements of `numberlist` plus all the elements of `stringlist`, giving us six items altogether.  Type `print(biglist)` to make sure that's the case.

In contrast, the statement `biglist2 = [numberlist, stringlist]` produces a new list with two items:  the lists `numberlist` and `stringlist`.  It's what we might call a "list of lists."  That's not something we're likely to do, to be honest.  (We did it once, but that was an accident.)  The point is simply that lists are flexible objects.


**Exercise.** How would you explain a list to a classmate?

**Exercise.** Add `print(numberlist)` and `print(variablelist)` to your code and note the format of the output.  What do the square brackets tell us?  The single quotes around some entries?


**Exercise.** Run the statements

```python
mixedlist = [a, b, c, numberlist]
print(mixedlist)
```

What is the output?  How would you explain it to a classmates?


**Exercise.** Suppose `x = [1, 2, 3]` is a list.  What is `x + x`? `2*x`?  Try them and see.


## Tuples

Tuples are ordered collections of things in parentheses separated by commas.  They're like lists but the syntax is different (parentheses rather than square brackets) and **they can't be changed** (experts would say they're "immutable").  We won't use them much but you're likely to run across them now and then in others' code.

**Example.**  This is a tuple: `t = (1, 5, -3)`.


## Python's built-in functions

We now have several kinds of **objects** to work with:  numbers, strings, and lists.  There are more on the way, but that's a good start.  And yes, the formal term is really **objects**.  But what can we do with them?  Python has two basic ways to express things we do with objects:  **functions** and **methods**.  We'll talk about functions in this section and methods in the next one.

Python has a lot of basic "built-in" functions.  We've already seen the `print()` function.  Here are some others we've found useful.

**The `len()` (length) function.**  This tells us the length of an object.  We can work this one out for ourselves:

**Exercise.**  Describe the output of typing each of these **one cell at a time**:

```python
len('hello')
len([1, 5, -3])
len((1, 5, -3))
len('1234')
len(1234)
len('12.34')
len(12.34)
```

What do you think is happening?


**The `type()` function.**  One of our favs.  This one tells us what kind of object we have.  To see how it works, type each of these **one cell at a time**:

```python
type(2)
type(2.5)
type('2.5')
type('something')
type([1, 5, -3])
type((1, 5, -3))
```

Think about this on your own for a minute. What do you think you'll get?  How does it compare to the real output?

Not to kill the suspense, but here's what we should see:

* `type(2)` gives us the output `int`, which stands for "integer,"  a whole number like 1, 2, 3, and so on.  Just to clarify: 2 is an integer. 2.5 is not.
* `type(2.5)` gives us `float`, a so-called "floating point number" like most of those we run across in Excel -- not a whole number.
* `type('2.5')` gives us `str`, a string because it's in quotes.
* `type('something')` also gives us `str`.
* `type([1, 5, -3])` gives us `list`.
* `type((1, 5, -3))` gives us `tuple`.


The type function is more helpful than you might guess.  A lot of what we do in programming is deal with objects of different types and, when necessary, convert one type to another.  The first step is to identify the type of the object of interest.

**Exercise.** Try each of these, one at a time, in a code cell and explain the output:

```python
type('a')
type('a1')
type('a1.0')
type(1)
type(1.0)
type('1')
type('1.0')
type([1, 5, 3])
type(['data', 'bootcamp'])
```

**Exercise.**  Try `type(zoo)`.  Why does it generate an error?  What does the error mean?

**Exercise.** Set `zoo = ['lions', 'bears']` and try `type(zoo)` again.  What do you get this time?


## Changing types

If we have an object of one type, we can sometimes change it to another type. (Sometimes it doesn't make sense and Python tells us so.) The string `'12'` can be converted to the integer `12`, for example.

**Converting strings to numbers.** Suppose we have an object of one type (the string `'12.34'`) and want to use it as another (the number `12.34`).  We can use the function `float()`, then use `type()` to check:

```python
s = '12.34'
f = float(s)
type(f)
```

Here `s` is a string but `f` is the floating point number `12.34`.

The function `int()` lets us do the same for integers. Convert the string `'12'` to an integer, then check with `type()` again:

```python
s = '12'
i = int(s)
type(i)
```

The result `i` is the integer 12.

**Converting numbers to strings.** Similarly, we can convert a number back to a string with `str()`:

```python
s = str(12)
print('s has type', type(s))
t = str(12.34)
print('t has type', type(t))
```

**Converting strings to lists.** One more type conversion:  We can convert a string to a list of its characters.  For example, we convert the string `x = abc'` to the list `['a', 'b', 'c']` with `list(x)`.  Run this code to see how it works:

```python
x = 'abc'
y = list(x)
print(y)
```

**Exercise.** What happens if we apply the function `float` to the string `'some'`?

**Exercise.**  How would you convert the integer `i = 1234` to the list `l = ['1', '2', '3', '4']`?

**Exercise.** What is the result of `list(str(int(float('12.34'))))`?  Why?  *Hint:* Start in the middle (the string `'12.34'`) and work your way out, one step at a time.

**Exercise (challenging).**  This one is tricky, but it came up in some work we were doing.  Suppose `year` is a string containing the year of a particular piece of data; for example, `year = '2015'`.  How would we construct a string for the following year?  *Hint:*  Start by converting year to an integer.


## Objects and methods

As we noted, lots of things in Python are **objects**.  **Methods** are ready-to-go things we can do with these objects.  The available methods depend on the object.  A lot of Python is "object-oriented," which means we apply methods to objects to accomplish what you might think you need a function for.  Trust us, the jargon is harder than just doing it.

<!--
	(Experts might say at this point:  an object is an "instance" of a "class."  Ignore them.)
-->

Functions and methods differ primarily in their syntax:

* Syntax of a **function**: `function(object)`
* Syntax of a **method**: `object.method`

We used the former in the previous section and consider the latter here.

What methods are available to work with a given object?  Take, for example, the list `numberlist = [1, 5, -3]`.  To get the list of available methods, type in a code cell:

```python
numberlist.[tab]    # here you hit the tab key, don't type in the word "tab"

```

This wonderful piece of technology is referred to as **tab completion**.  The ingredients here are the object (here `numberlist`), the period or dot, and the tab key.  When you hit tab, a window will pop up with a list of methods in alphabetical order.  In our example, the list starts like this:

```python
numberlist.append
numberlist.clear
numberlist.copy
numberlist.count
```

If we want more information about a method, we can type `object.method?` in a code cell.  For the method `numberlist.append`, we get the description

```python
Definition:  append(object)
Type:  Function of None module
L.append(object) -> None -- append object to end.
```

Well, that's pretty opaque, maybe we oversold this approach.  What `append` does is add an item to the end of a list.  Try using `append()`, then use `print()` to see the results:

```python
numberlist.append(7)
print(numberlist)
```

That's another way to get information about a method: try it and see what happens.


**Digression.**  We're trying to keep this simple, but we also want it to be accurate, so let us be more careful with the term **method**.  Needless to say, this is **mtwn**.  Tab completion gives us a list of two things:  *attributes* (properties of the object) and *methods* (essentially functions with different syntax).  The distinction isn't important to us, although we can tell a method because it comes with parentheses `()` (just like functions).


**Example.** Set `firstname = 'Chase'`.  The method `lower` converts it to lower case.  If we type `firstname.lower` into the object inspector, we see that it comes with parentheses for additional inputs.  So we type `firstname.lower()` into a code cell.  The response is `'chase'`.  The parentheses are there to provide additional inputs -- arguments, we call them.  Without the parentheses, it doesn't work.


**Exercise.** Find a method to convert `firstname` to all upper case letters.

**Exercise.** This one also came up in our work.  Suppose we have a variable `z = '12,345.6'`.  What is its type?  Convert it to a floating point number without the comma.  Hint:  Use tab completion to find a method to get rid of the comma.

<!-- z = z.replace(',', '') -->

**Exercise.**  Run the code

```python
firstname = 'John'
lastname  = 'Lennon'
firstlast = firstname + ' ' + lastname
```

Find a method to replace the n's in `firstlast` with asterisks.


## Python 2 and 3

There's a lot of code around written in earlier versions of Python, most commonly Python 2.7.  It's there because the people who wrote it started before Python 3 was up and running.  Since we're starting from scratch, we are planting ourselves firmly in Python 3 territory.  Still, you're likely to run across examples of Python 2 on the internet. The easiest way to tell the difference is the print command:  `print(x)` in Python 3 was `print x` (no parentheses) in Python 2.  There are some other differences (more technical than we care to discuss), which is why it's essential we all use Python 3.


## Review

Work with your neighbor on these review exercises:

**Exercise.** Take turns with your neighbor explaining these terms:
integer, float, string, list, tuple, function, method, tab completion.

**Exercise.** What types are these expressions?  What lengths?

```python
a = 1234
b = 12.34
c = '12.34'
d = [1, 2, 3, 4]
e = (1, 2, 3, 4)
```

**Exercise.** Describe the results of these operations:

```python
a + b
a + c
d + d
d.append(a)
```

**Exercise.** Describe the results of these operations:

```python
str(float('3.1416'))
str(int('3.1416'))
str(len('3.1416'))
str(len(3.1416))
```

**Exercise.** Set `name = 'Jones'`.  Use (a) tab completion to find a method that coverts `name` to upper case (capital) letters and (b) the Object inspector to find out how to use that method.  *Bonus:* How else can you get help in Spyder for methods and functions?

**Exercise (challenging).** Use tab completion and the Object inspector to find and apply a method to the string `name` that counts the number of appearances of the letter s.  Use `name = 'Ulysses'` as a test case.

**Exercise (challenging).** Describe the result of `list(zip('1234','abcd'))`.


## Resources


If you'd like another source for comparison, here are some good introductions to basic Python and related topics:

* Codecademy has an excellent [Introduction to Python](http://www.codecademy.com/en/tracks/python).  You run Python in their online environment, which is really helpful when you're starting out. It uses Python 2, so the print statement has the form `print x` rather than `print(x)`.  If we were to recommend one outside resource, this would be it.  You should think seriously of working your way through it in parallel with this course.  If you do, you can stop (as far as this course in concerned) when you get to Advanced Topics.
* Here's a [list of free tutorials](http://noeticforce.com/best-free-tutorials-to-learn-python-pdfs-ebooks-online-interactive), but we think you can stop with the first one, Codecademy.
* The official [Python tutorial](\href{https://docs.python.org/3.4/tutorial/introduction.html) is very good.  It's also a good idea to get used to reading official documentation like this.  There are times when it's unavoidable.
* Mark Lutz's [Learning Python](http://www.amazon.com/Learning-Python-5th-Mark-Lutz/dp/1449355730/) is a 1600-page monster that covers lots of things we won't use.  But it's clear and thorough, and comes with the elusive Glenn Okun stamp of approval.  He tells us the Kindle version comes with free updates.

<!--
Python for humanities, solid intro:  http://fbkarsdorp.github.io/python-course/
-->

<!--
* Sebastian Raschka has more than you'll ever need  about the [differences between Python 2 and 3](http://sebastianraschka.com/Articles/2014_python_2_3_key_diff.html).
-->

These sources go well beyond what we do in this chapter, but we'll catch up with some of it later on.
