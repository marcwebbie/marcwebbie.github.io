title: Scrap The Web With PyQuery
category: tutorials
tags:
- Programming
- Python
- Scraping
- WebMining
---


In this article I will be showing how to do [Web Scraping](http://en.wikipedia.org/wiki/Web_scraping) in Python using Pyquery. There is a lot of [tools](http://docs.python-guide.org/en/latest/scenarios/scrape/) for webscraping using Python. The most well know tool is [Scrapy](http://scrapy.org/), Scrapy is a great tool, and you can find a lot of tutorials about it. Although Scrapy is a great tool, as of today Scrapy [doesn't support Python 3](http://doc.scrapy.org/en/latest/faq.html#does-scrapy-work-with-python-3) yet. Scrapy is also a framework, with a lot of functionalities and a particular directory structure that you should use. Those are the makor points that hold me back from using Scrapy for most of my web scraping.

Most of the time my Web Scraping code can be sumarized to the steps:

1. Go to x url
2. Find elements "foo", "bar", etc
3. Build data from found elements

For this kind of application, I only need one tool:

## Pyquery

[PyQuery](https://github.com/gawel/pyquery/) lets you access webpage elements in using the DOM similar to the way [JQuery](http://jquery.com/) do it. Check those examples:


#### `html`

Suppose that the content of example.com is the html below:

``` html example1.html
<ul>
  <li>foo</li>
  <li>bar</li>
</ul>
```

#### `JQuery`

``` javascript example1.js
// example from http://api.jquery.com/each/
$( "li" ).each(function( index ) {
  console.log( $( this ).text() );
});
```

#### `PyQuery`

``` python example1.py
from pyquery import PyQuery
d = PyQuery("example.com")
for li in d("li"):
    print(li.text)
```

`d` in our `example.py` works the same as our `$` at example.js. One big bonus is not having to use another library to download page content. PyQuery can fetch it for you:

    d = PyQuery("http://www.example.com")

Here `d` is a referencing the dom on the content of `www.example.com`.

Cool right? **PyQuery** has much of JQuery syntax and even some unique constructs. Most of the time you can test your constructs on your browser console and copy past the selectors string into your python code.

Mixing PyQuery with [Requests](http://docs.python-requests.org/en/latest/) makes Web Scraping even more powerful. When the need comes to interact with the web page, like send forms, manage cookies and more, Requests + Pyquery will be the couple of tools you will need.


## Getting started

We will create `fooscraper`. `fooscraper` will be a little tool that finds every hred links in a webpage and download the page that it points. Not very useful as an application but it will show you the idea behind PyQuery

The tools needed:

+ [pip](https://pypi.python.org/pypi/pip/)
+ [virtualenv](https://pypi.python.org/pypi/virtualenv)


### Create and activate virtualenv

Let's use a virtualenv for isolating work from the system:

    virtualenv scraping
    cd scraping
    source bin/activate


#### Create project files

Now that our virtualenv active, let's create our project files:

    mkdir fooscraper
    cd fooscraper
    touch fooscraper.py
    touch tests.py


#### Install PyQuery

    pip install pyquery

------

### Scraping


#### Step 1 - Find all links in a page

Find all `<a>` links on the webpage at the given url and return them as a list of urls to resources:

``` python archive.py
from pyquery import PyQuery
#...
def find_links(url):
    d = PyQuery(url)
    return [d(a).attr("href") for a in d("a")]
```


#### Step 2 - Find only internal links

Let's make our find links code cleaner to get only internal links:

``` python archive.py
def is_absolute(url):
    return bool(urlparse(url).netloc)


def find_links(url):
    d = PyQuery(url)
    return [d(a).attr("href") for a in d("a")
            if not is_absolute(d(a).attr("href"))]
```


#### Step 3 - Download every resouce at link into path

Save every resource located at path into a file inside given path:

``` python archive.py
# previous snippets
# ...
def download(url, link, directory):
    resource_url = urljoin(url, link)
    content = urlopen(resource_url)
    filepath = path.join(directory, link)
    with open(filepath, "w") as f:
        f.write(content)
    return filepath
```


#### Step 4 - Main entry to download all links

```
# previous snippets
# ...
if __name__ == "__main__":
    parser = argparse.ArgumentParser(prog="fooscraper")
    parser.add_argument("url", help="Url to look for links")
    parser.add_argument("-d", "--download", action="store_true",
                        help="Url to look for links")
    args = parser.parse_args()
    #
    download_dir = "data"
    if not os.path.exists(download_dir):
        os.makedirs(download_dir)
    #
    links = find_links(args.url)
    if args.download:
        for link in find_links(args.url):
            dl_path = download(args.url, link=link, path=download_dir)
            print("Saved file into {}".format(dl_path))

```


You can run the code from terminal:

    fooscraper example.com

or to download all links into a a given path

    fooscraper -d /tmp/save_dir example.com

#### Async downloads

If you want to download the pages asynchronously, we can use a decorator

``` python decorators.py
from threading import Thread
#
def async(f):
    def wrapper(*args, **kwargs):
        thr = Thread(target=f, args=args, kwargs=kwargs)
        thr.start()
    return wrapper
```

Then apply the decorator to the Download Method:

``` python archive.py
from decorators.py import async
# previous snippets
@async
def download(url, link, directory):
    resource_url = urljoin(url, link)
    content = urlopen(resource_url)
    filepath = path.join(directory, link)
    with open(filepath, "w") as f:
        f.write(content)
    return filepath
```

## Summary

Of course PyQuery is much more useful than that. I've been using it for a while now and it has fulfilled much of my needs in Web Scraping. Their
[documentation](https://pythonhosted.org/pyquery/index.html) is very concise and easy to read. Their code is also very clean. Bonus points if you read it at [Github](https://github.com/gawel/pyquery).

PyQuery as described on their page:

> allows you to make jquery queries on xml documents. The API is as much as possible the similar to jquery. pyquery uses lxml for fast xml and html manipulation.

And it seems that there is more to come:

> It can be used for many purposes, one idea that I might try in the future is to use it for templating with pure http templates that you modify using pyquery. I can also be used for web scrapping or for theming applications with [Deliverance](https://pythonhosted.org/Deliverance/).


## Links

- [Source code](http://localhost)
- [PyQuery docs](https://pythonhosted.org/pyquery/index.html)
- [Requests](https://pythonhosted.org/pyquery/index.html)
- [Scrapy](http://scrapy.org)
- [Scraping Tutorial](http://blog.miguelgrinberg.com/post/easy-web-scraping-with-python)
