---
layout: post
title:  "Argument parsers statistics"
date:   2016-05-13 16:12:27 +0300
categories: jekyll update
---
Common Workflow Language command line tools mostly consist of input/output parameters descriptions. These descriptions often can be created automatically directly from the code of the actual Python tool. The more information is provided in the source code of the tool, the less has to be written by hand in a CWL tool description. 


The amount of information about tool arguments is defined by its argument parser. Different argument parsers have different syntax and verbosity level, that's why it is important to know:

a) which argument parsers are used most frequently;

b) which ones provide the most information that could be used in forming CWL command line tools.

After a brief overview I have selected 5 most popular ways to parse command line arguments in Python:

#### sys.argv 

Standart module `sys` provides the most straightforward way to parse command line arguments, simply putting all of them into a list, disregardless of their characteristics. This is the the least flexible way to deal with arguments, but due to its simplicity and universality it is very popular

#### argparse 

This is a standard module in Python since version 2.7. It has a lot of advantages over its predecessor `optparse`, such as handling positional arguments, supporting sub-commands, producing more informative usage messages. For now it is the most convenient way to obtain information about parameters and to form CWL tool out of it. 

#### optparse 

A deprecated but still used module in old projects.

#### docopt 

A library for "creating beautiful command-line interfaces", as claimed by its developers. It uses just a few lines of code to generate a parser, and requires a well-written docstring.

#### click 

A library which is considered by some more intuitive, lightweight than argparse and at least as powerful.

I was curious about which libraries are the most wide-spread in bioinformatics community. That's why I wrote a simple program to gather some statistic from github repositories. I parsed a list of bioinformatics repositories from [Python Package Index][pypi], grabbed links to GitHub sources and counted a number of files where each of the above libraries is imported. The source code is available [here][bitbucket].

The results are the following:

<table cellpadding="10" frame="void" rules="all" style="border: 1px solid black;">
    <tr>
        <td>optparse</td>
        <td>130 files</td>
    </tr>
    <tr>
        <td>docopt </td>
        <td>47 files</td>
    </tr>
    <tr>
        <td>argparse</td>
        <td>727 files</td>
    </tr>
    <tr>
        <td>argv</td>
        <td>804 files</td>
    </tr>
    <tr>
        <td>click</td>
        <td>85 files</td>
    </tr>
</table>

![My helpful screenshot](/argparse2cwl-blog//assets/bar.png)

So, the most popular argument parsers are the standart libraries: `sys.argv` and `argparse` exceed other libraries by number at least by five times.

It was also interesting to look at argument parsers in context of the popularity of the repositories. Here is the plot which represents occurences of argument parsers in different repositories regarding the number of their downloads, a dot means the presense of library in a repository. 
![My helpful screenshot](/argparse2cwl-blog//assets/scattered.png)
There are much more `sys.argv` dots than `argparse` dots, though the number of files is pretty close; it means that projects that don't use argument parsers intensively, one or two times per project, tend to use `sys.argv`. It is also more widespread among popular repositories, but I looked through some of them and they tend to use argument parsers in targets others than bio tools which I am supposed to convert.


In general, the statistics show that argparse2cwl project has good chances to be useful for a wide circle of cases. Even though the most popular argument parser is not appropriate for processing, there are more than enought tools which use `argparse`. Nevertheless, the number of usages of other argument parsers is not so insignificant to neglect them, so it would be nice to add their support too.


[pypi]: https://pypi.python.org/pypi?:action=browse&show=all&c=388
[bitbucket]: https://bitbucket.org/anton-khodak/parser-survey
