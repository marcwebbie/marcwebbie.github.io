title: Write your code in Python 3
date: 2014-12-29 21:52:21
category:
- Programming
tags:
- Python
- Porting
- Python3
---

[Python 3](https://www.python.org/download/releases/3.0/) is there since 2008. However, we still find a lot of projects that doesn't run on Python3. I've started programming in Python 3 when I started using [Arch Linux](https://www.archlinux.org/) as my main linux distribution a few years ago.


![](python3.svg)

----------


## Why Python 3?

Python 3 is the future of python. With Python 3 you will get all the [cool features](http://asmeurer.github.io/python3-presentation/slides.html#1) that are being added to the language. Core python developers have been focusing in Python 3 for a while now, and you should be using those features into your projects.

Around the web I've seen many guesses on why Python 3 wasn't fully adopted until now. This [answer](http://programmers.stackexchange.com/a/63935) on StackExchange is quite a good starting point to know more.


## Starting With Python 3

When you are starting a new project. Start it in **`Python3`**. You may hear people say to you: *"Don't use Python 3, library x and y is not supported"* or worse, *"Why Python 3? Python 2 is much better"*...

Most of great libraries and frameworks [supports Python 3](https://python3wos.appspot.com/) already. If they are not. They are probably working on [fixing this](Twisted is already) situation right now. And you could help them if you have some sparetime. Check their issue pages. Starting a project in **`Python2`** today is probably not a good idea.

The first step to start a project in python **`Python3`** should be adopting the **"Python3 Mindset"**. Having a "Python3 Mindset" means, thinking in **`Python3`** without coding the way that you used to in **`Python2`**. The more the time goes by, more libraries will be ported/available to **`Python3`**, so the "burden" of having to support **`Python2`** code progressively fades away.


### Imcompatible Python 2 Code

Python 3 has a new safe input function: `input()`. In Python 2 however, `input()` evaluates user entry:

##### `Python2`

    >>> entry = input("Enter something: ")
    Enter something: 123
    >>> type(entry)
    <type 'int'>

##### `Python3`

    >>> entry = input("Enter something: ")
    Enter something: 123
    >>> type(entry)
    <type 'str'>

If for example you need to have the same functionality from Python 3 `input` function in Python 2, you should use `raw_input("Enter something: ")` instead.

##### `Python2`

    >>> entry = raw_input("Enter something: ")
    Enter something: 123
    >>> type(entry)
    <type 'str'>

### Using a compatibility module

If you need to support Python 2, maybe because a library you have to use wasn't still fully ported to Python 3. You could use a compatibilty module inside your packages.

For example for a compatibility module `python_two.py`:


    . mymodule
    ├── README.rst
    ├── docs
    ├── MANIFEST.in
    ├── myprogram
    │   ├── __init__.py
    │   ├── downloader.py
    │   ├── python_two.py  # <== This is the compatibility module
    │   └── utils.py
    ├── requirements.txt
    ├── setup.cfg
    ├── setup.py
    └── tests
        └── test.py

Write code that fallback to Python 2. An example `python_two.py` could be:

~~~python
from __future___ import print_function
...
try:
    input = raw_input
    str = unicode
    range = xrange
except NameError:
    pass
...
try:
    from io import StringIO
    from unittest.mock import Mock
except ImportError:
    import StringIO
    from mock i
~~~

If in the `downloader.py` module you ask for user input:

~~~python
from .python_two import input, range, str
~~~

-OR-

~~~python
from .python_two import *
~~~


Using the compatibility module with our earlier example:

##### `Python2`

    >>> from .python_two import input
    >>> entry = input("Enter something: ")
    Enter something: 123
    >>> type(entry)
    <type 'str'>

The idea is to remove this module when you decide not to support Python 2 any longer.


### Using 2to3 on Python 2 code

You can also use a tool called [2to3](http://www.diveintopython3.net/porting-code-to-python-3-with-2to3.html) to port your code. Python 3 comes with 2to3 out of the box.

An example module `mymodule.py`:

##### `Python2`

~~~python
import urllib
# ...
value = range(1, 10)[-1]
# ...
if value <> 9:
    print "Value %s is not 9" % value
else:
    print "Value is 9"
# ...
try:
    assert 1 == 2
except AssertionError, e:
    print e
    print urllib.urlopen('https://docs.python.org/2/library/exceptions.html').read()
~~~


When you run **2to3** `2to3 mymodule.py -w` the results are:

##### `Python3`

~~~python
import urllib.request, urllib.parse, urllib.error
# ...
value = list(range(1, 10))[-1]
# ...
if value != 9:
    print("Value %s is not 9" % value)
else:
    print("Value is 9")
# ...
try:
    assert 1 == 2
except AssertionError as e:
    print(e)
    print(urllib.request.urlopen('https://docs.python.org/2/library/exceptions.html').read())
~~~

**2to3** is a great tool to migrate existing `Python2` code. If you project is still in its early days, **2to3** may come handy as a tool.

### Start your project in Python 2 then...

Please, **NOT** so fast! If you have options, start with Python 3 from day one. It will be much harder to port your project to Python 3 once the project gets larger. Check this [presentation](https://speakerdeck.com/pyconslides/python-3-dot-3-trust-me-its-better-than-python-2-dot-7-by-dr-brett-cannon) by Brett Cannon to see why Python 3 is much better or his [video](https://www.youtube.com/watch?v=f_6vDi7ywuA) presentation if you prefer.


## Workflow

An example workflow for a Python 3 code that is backward compatible with Python 2 would be:

1. Write **`Python3`** code.
2. Run your tests/code in **`Python3`**
   + If broken, go to **step 1**.
3. Run your tests/code using **`Python2`**.
   + If broken, update your `python_two.py` module and go to **step 2**.
4. Commit and go to **step 1**.


## Learn more

There is a large amount of information about Python 3 around the web:

+ [Python 3 Wall of Superpowers](https://python3wos.appspot.com/)
+ [Python wiki](https://wiki.python.org/moin/Python2orPython3)
+ [Porting to python 3]()
+ [PyVideos](http://pyvideo.org)

There are also some great books on the subject:

+ [Python Cookbook 3rd Edition](http://chimera.labs.oreilly.com/books/1230000000393)
+ [Dive into Python 3](http://www.diveintopython3.net/)
+ [Porting to Python 3](http://python3porting.com)

Some videos as well:

+ [Python 3 Metaprogramming](https://www.youtube.com/watch?v=sPiWg5jSoZI)
+ [Python 3 - Trust Me, It is Better than Python 2](https://www.youtube.com/watch?v=sPiWg5jSoZI)
