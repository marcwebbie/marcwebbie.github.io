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


## Starting With Python3

When you are starting a new project. Start it in Python 3. You may hear people say to you: *"Don't use Python 3, library x and y is not supported"* or worse, *"Why Python 3? Python 2 is much better"*. Don't listen to those comments. Most of great libraries and frameworks [supports Python 3](https://python3wos.appspot.com/) already. If they are not. They are probably working on [fixing this](Twisted is already) situation right now. And you could help them if you have some sparetime. Check their issue pages. Starting a project in Python 2 today is probably not a good idea.


If you need to support people running on python 2. Use a compatibilty module `python_two.py` inside your package. For example:

```
├── README.rst
├── docs
├── MANIFEST.in
├── myprogram
│   ├── __init__.py
│   ├── __main__.py
│   ├── downloader.py
│   ├── python_two.py  # <== This is the compatibility module
│   └── utils.py
├── requirements.txt
├── setup.cfg
├── setup.py
├── testing.py
└── tests
```


In the compatibilty module. Write code that fallback to Python 2. For example if in your downloader module you ask for user input. Python 3 has a new safe input function: `input()`. In Python 2 however, `input()` will try to evaluate user entry:


Python2:

```python
>>> entry = input("Enter something: ")
Enter something: 123
>>> type(entry)
<type 'int'>
```

Python3:

```python
>>> entry = input("Enter something: ")
Enter something: 123
>>> type(entry)
<type 'str'>
```

A good `python_two.py` module could be something like that:

```python
# python_two.py
from __future___ import print_function
try:
    input = raw_input
    str = unicode
    range = xrange
except NameError:
    pass

try:
    from io import StringIO
    from unittest.mock import Mock
except ImportError:
    import StringIO
    from mock i
    ```

From your modules that have to use the compatible code you could do:

```python
# .downloader.py
from .python_two import input, range


# ... your code goes here
```

The idea is to remove this module when you decide not to support Python 2 any longer.

## Start your code in Python 2 then...

Please **don't**! If you can do it, start it on Python 3. It will be much harder to port your project to Python 3 once the project gets larger. Check this [presentation](https://speakerdeck.com/pyconslides/python-3-dot-3-trust-me-its-better-than-python-2-dot-7-by-dr-brett-cannon) by Brett Cannon to see why Python 3 is much better or his [video](https://www.youtube.com/watch?v=f_6vDi7ywuA) presentation if you prefer.


## Learn more

There are a large amount of information about Python 3 around the web:

+ [Python wiki](https://wiki.python.org/moin/Python2orPython3)
+ Porting to python 3
+ [Python 3 Wall of Super Powers](https://python3wos.appspot.com/)
+ [PyVideos](http://pyvideo.org)

There are also some great books on the subject:

+ [Python Cookbook 3rd Edition](http://chimera.labs.oreilly.com/books/1230000000393)
+ [Dive into Python 3](http://www.diveintopython3.net/)
+ [Porting to Python 3](http://python3porting.com)

Some videos as well:

+ [Python 3 Metaprogramming](https://www.youtube.com/watch?v=sPiWg5jSoZI)
+ [Python 3 - Trust Me, It is Better than Python 2](https://www.youtube.com/watch?v=sPiWg5jSoZI)
