---
layout: post
title:  "Argument parsers statistics"
date:   2016-05-13 16:12:27 +0300
comments: true
---
<a href="http://www.commonwl.org/">Common Workflow Language</a> <a href="http://www.commonwl.org/draft-3/CommandLineTool.html">command line tools</a> mostly consist of input/output parameters descriptions. These descriptions could be created automatically and directly from the code of the actual Python tool. The more information is provided in the source code of the tool, the less has to be written by hand in a CWL tool description. 


The amount of information about tool arguments is defined by its argument parser. Different argument parsers have different syntax and verbosity level, that's why it is important to know:

a) which argument parsers are used most frequently;

b) which ones provide the most information that could be used in forming CWL command line tools.

After a brief overview I have selected 5 most popular ways to parse command line arguments in Python:

#### sys.argv 

Standard module `sys` provides the most straightforward way to parse command line arguments, simply putting all of them into a list, regardless of their characteristics. This is the least flexible way to deal with arguments, but due to its simplicity and universality, it is very popular

#### argparse 

This is a standard module in Python since version 2.7. It has a lot of advantages over its predecessor `optparse`, such as handling positional arguments, supporting sub-commands, producing more informative usage messages. For now, it is the most convenient way to obtain information about parameters and to form CWL tool out of it. 

#### optparse 

A deprecated but still used module in old projects.

#### docopt 

A library for "creating beautiful command-line interfaces", as claimed by its developers. It uses just a few lines of code to generate a parser and requires a well-written docstring.

#### click 

A library which is considered by some more intuitive, lightweight than argparse and at least as powerful.

I was curious about which libraries are the most wide-spread in the bioinformatics community. That's why I wrote a simple program to gather some statistic from GitHub repositories. I parsed a list of bioinformatics repositories from <a href="https://pypi.python.org/pypi?:action=browse&show=all&c=388">Python Package Index</a>, grabbed links to GitHub sources and counted a number of files where each of the above libraries is imported. The source code is available <a href="https://bitbucket.org/anton-khodak/parser-survey">here</a>.

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

So, the most popular argument parsers are the standard libraries: `sys.argv` and `argparse` exceed other libraries by number at least by five times.

It was also interesting to look at argument parsers in the context of the popularity of the repositories. Here is the plot which represents occurrences of argument parsers in different repositories regarding the number of their downloads over the last month, a dot means the presence of a library in a repository. 
![My helpful screenshot](/argparse2cwl-blog//assets/scattered.png)
There are much more `sys.argv` dots than `argparse` dots, though the number of files is pretty close; it means that projects that don't use argument parsers intensively, one or two times per project, tend to use `sys.argv`. It is also more widespread among popular repositories, but I looked through some of them, and they tend to use argument parsers in targets others than bio tools which I am supposed to convert.

A useful outcome for the project: top 10 repositories which use argparse.
<table cellpadding="10" frame="void" rules="all" style="border: 1px solid black;">
<tr><td>Name</td><td>Description</td><td>Argparse</td><td>Downloads</td></tr>
<tr><td><a href="https://github.com/genialis/resolwe-bio/">resolwe-bio</a></td><td>Bioinformatics pipelines for the Resolwe platform.</td><td>37</td> <td>722</td></tr>
<tr><td><a href="https://github.com/sanger-pathogens/Fastaq">pyfastaq</a></td><td>Script to manipulate FASTA and FASTQ files, plus API for developers</td><td>37</td> <td>1043</td></tr>
<tr><td><a href="https://github.com/mjirik/lisa">lisa</a></td><td>3D data processing toolbox</td><td>36</td> <td>1069</td></tr>
<tr><td><a href="https://github.com/hall-lab/svtools">svtools</a></td><td>Tools for processing and analyzing structural variants</td><td>27</td> <td>230</td></tr>
<tr><td><a href="https://github.com/lemieuxl/pyGenClean">pyGenClean</a></td><td>Automated data clean up pipeline for genetic data</td><td>26</td> <td>353</td></tr>
<tr><td><a href="https://github.com/smdabdoub/phylotoast">phylotoast</a></td><td>Useful additions to the QIIME analysis pipeline including tools for data visualization and cluster-computing.</td><td>25</td> <td>98</td></tr>
<tr><td><a href="https://github.com/OpenTreeOfLife/peyotl">peyotl</a></td><td>Library for interacting with Open Tree of Life resources</td><td>23</td> <td>31</td></tr>
<tr><td><a href="https://github.com/joshuagryphon/plastid">plastid</a></td><td>Convert genomic datatypes into Pythonic objects useful to the SciPy stack</td><td>18</td> <td>287</td></tr>
<tr><td><a href="https://github.com/fhcrc/taxtastic">taxtastic</a></td><td>Tools for taxonomic naming and annotation</td><td>17</td> <td>267</td></tr>
<tr><td><a href="https://github.com/StanfordBioinformatics/loom">loom-engine</a></td><td>loom workflow engine</td><td>15</td> <td>53</td></tr>
</table>
<br>
In general, the statistics shows that <a href="https://github.com/common-workflow-language/gxargparse/tree/cwl-refactor">argparse2cwl</a> project has good chances to be useful for a wide circle of cases. Even though the most popular argument parser is not appropriate for processing, there are more than enough tools which use `argparse`. Nevertheless, the number of usages of other argument parsers is not so insignificant to neglect them, so it would be nice to add their support too.


{% include disqus.html %}


