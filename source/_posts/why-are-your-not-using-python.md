title: Why Are You Still Not Using Python?
category:
- Python
tags:
- Python
- Projects
- History
- Programming
- Programming Languages
---

Today we have hundreds(if not thousands) of programming languages and many more are built everyday. We have people that don't care about languages, we have fanboys. One thing is certain, every developer has their own favorite language.

How do you catch up with languages? Which languages to choose for your next project?

Some companies decide on the language they will implement their next application because they believe it will be easier to support their legacy mainframe code. Some others decide on it because they believe that since a big company has written the language they will be big as well. Some even decide on the language because they think it is cool to code in that language and they will attract the best talents. Most of the time they could only use Python and be happy about it.

>But I just need to write a simple script that goes to my server and download some files...

**Answer**: Python

>But I just want to write a simple web application where we can sell our beautiful carpets online...

**Answer**: Python

>But I need to write that interface to our 1-trillion-dollars-large-dinosaur-communication system...

**Answer**: Python

Ok, ok, I may sound a bit extreme, but please, keep reading...

## Python

Python is today more than 20 years old and it is one of the most used languages in the world. Python is powering from spacial applications from nasa to first-person shooters like [Battlefield](http://www.battlefield.com/) or even helping mathematicians research.

From wikipedia:

>The history of the Python programming language dates back to the late 1980s.

>Python was conceived in the late 1980s[1] and its implementation was started in December 1989[2] by Guido van Rossum at CWI in the Netherlands as a successor to the ABC programming language capable of exception handling and interfacing with the Amoeba operating system.[3] Van Rossum is Python's principal author, and his continuing central role in deciding the direction of Python is reflected in the title given to him by the Python community, Benevolent Dictator for Life (BDFL).


## What is so good about Python?

#### Python is fast to develop

Python code is normally a lot shorter than other languages code. Shorter code doesn't mean hard to understand code. It means that the developer writes less code than they would some other languages to acomplish the same tasks.

If you've heard about the game [Minecraft](https://minecraft.net/). You can check a simple implementation of that same game writen in less than 1000 lines of Python code on [Github](https://github.com/fogleman/Minecraft).


#### Python is easy to read

Python code is cleaner and easy to read. Python lovers call themselves [Pythonistas](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html) and those Pythonistas follow the rules found on the [Zen of Python](https://www.python.org/doc/humor/#the-zen-of-python). Python is pretty high level, which means that you write less programmers-only understandable code

For example to print the numbers from 0 to 99:

##### `C++`

``` c++
#include <stdout>
for(int number=0; number<=99; ++number){
    std::cout << "Number: " << number << std::endl;
}
```

##### `Python`

``` python
for number in range(1000):
    print("Number: " + number)
```

Even if you are not a programmer, which one you think it is easier to read?

#### Python is easy to maintain

Python has a great [documentation](https://docs.python.org) and lots of libraries written for various tasks. From [database drivers](https://wiki.python.org/moin/DatabaseInterfaces) to [audio manipulation](https://wiki.python.org/moin/Audio)

Python programmers most of the time don't need to worry about memory management or other kind of low level implementation as some other language programmers have to think about day and night.


#### Python is multi-platform

Python supports almost all platforms available today. If the computer you will be running has a processor, then python runs on it.


#### Python is free and not owned by someone


Python is not owned by some big companies that decide on when they will do something to Python. Python is open and free. Python code is available online and you can read it. Actually, Python implementation code is also incredibly easy to read, as you might have thought.

#### Python has a lot of stuff built in

Python standard libray has a lot of functionalities builtin. Great examples of what you can do with pure python is math, network, system programming, game development.

Python has facilities to access websites, databases, csv, graphics, text processing and many other stuff.


#### Python is well maintained

Python is maintained by developers from Python Software Foundation. [Guido Van Rossum](https://www.python.org/~guido/), Python creator, has still an important role in the language implementations.

Python language is enhanced using [PEPs](https://www.python.org/dev/peps/). PEPs are Python Enhacement Proposals and it is open and great way of handling propositions for language features.


#### Python has a great community

Python community is easy going. Python is considered one of the best languages to start programming and this fact alone makes people much more open to beginners questions around. You can easily get that "noob" question answered in the community. IRC channel #python at [freenode](https://freenode.net/) is the main channel where you can find pythonistas to discuss.

## But language X has more developers...

Choosing a language because there are more developers available sounds like a good idea in the beginning. *"We will have more people available in case we need to hire more people"* they say. The point here is that it might be easier to find language X or Y programmers, but is it easy to keep this programmers when your code is dinausor with 10 million lines and hundreds of issues about memory management or 7000 lines functions? Yes, I said 7000 lines functions, I've seen that already. :P

Do you really think that developers will want to stay and built great applications with you if they have to manage this kind of situation? I am not saying that all non python applications are this mess, but I am sure that this kind of mess is hard to find in Python code.


## Who is using python then?

+ [Instagram](https://instagram.com) - Written in Python with Django
+ [Dropbox](https://dropbox.com) - Written in Python
+ [Disqus](http://disqus.com) - Written in Python with Django
+ [Reddit](https://reddit.org) - Written in python
+ [Facebook](https://facebook.com) - Uses Tornado server to support their application, which is written in Python
+ [Mozilla](https://www.mozilla.org/en-US) - Uses python in their webapplications. Ex: https://developer.mozilla.org/fr/
+ [Red Hat](http://www.redhat.com/en) - Uses Python for its installer (anaconda) and configuration utilities.
+ [Pinterest](https://www.pinterest.com/) - Uses Python for their server.
+ [NASA](http://www.nasa.gov/) - Uses python in many applications, such as they [Integrated Planning System](http://ti.arc.nasa.gov/tech/asr/planning-and-scheduling/)
+ [Google](https://google.com) - Uses python extensively, from Google App Engine, Google groups to Youtube
+ [Yahoo](https://yahoo.com) - Yahoo maps uses python
+ [IBM](http://ibm.com) - IBM East Fishkill is using Python to create the business practice logic for factory tool control applications.

Want more? Check this https://wiki.python.org/moin/OrganizationsUsingPython

## Ok, so Python 3 or Python 2?

**Python 3**. You should start your project in Python 3. You shouldn't be worrying about this before starting since your choice should be Python 3.

If you've found a great library that is not supported in Python 3 yet, either search a little deeper(You might be surprised) or help them supporting Python 3.

## Is that all?

Of course not, Python is a multi-purpose language, it can solve a lot of problems you may have right now. Look further for how python can help you accomplish your goals.

### Where to start?

+ [Python website](https://python.org)
+ [Python success stories](https://www.python.org/about/success/)

#### Videos

+ [Full stack Python Web Applications](http://pyvideo.org/video/2591/so-you-want-to-be-a-full-stack-developer-how-to)
+ [PyVideo](http://www.pyvideo.org/)
