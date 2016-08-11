---
layout: post
title:  "GSoC Project Summary"
date:   2016-08-11 18:44:27 +0300
comments: true
---
Google Summer of Code 2016 is approaching to its finish line. Time to sum up what has been completed!

The original purpose of the project was to implement [Automated tool wrapper/converter for CWL](http://obf.github.io/GSoC/ideas/#automated-tool-wrapperconverter-for-cwl). That means, having a Python command-line tool that uses *argparse* standard library, a developer can automatically generate a tool written in [Common Workflow Language](http://www.commonwl.org/). The aim is to facilitate adapting new tools for CWL due to a great reduction of manual work on re-writing big numbers of arguments and tools. A good example is a [CNVkit](https://github.com/etal/cnvkit) - the toolkit of 30 tools with a number of arguments from 2 to 21. Now all of them are wrapped in CWL instantly, here are the __[results](https://github.com/common-workflow-language/gxargparse/tree/click/examples/argparse/cnvkit-tools)__.

The implementation of the tool wrapper was based on __[gxargparse](https://github.com/common-workflow-language/gxargparse)__ - a tool which solves a similar problem: generating [Galaxy XML](https://wiki.galaxyproject.org/Admin/Tools/ToolConfigSyntax) from Python tools. Having the base architecture for a new functionality, I have completed the initial task already before the midterm evaluation. The new *argparse2cwl* functionality embraces the whole argparse API and all parts of CWL where a correspondence can be established, all of this tested with a broad test case. Here is a pull request with all the commits regarding argparse2cwl: __[link](https://github.com/common-workflow-language/gxargparse/pull/13)__

After the midterm, my mentors brainstormed __[some new ideas](http://blogs.nopcode.org/brainstorm/2016/06/16/gsoc-2016-post-midterm)__ for the second half. The first in the row was __[pypi2cwl](https://github.com/common-workflow-language/pypi2cwl)__. It is a thin command-line wrapper around argparse2cwl that allows wrapping a PyPi package(s) without a need to install it and look for scripts. That could be used for bulk conversion when several packages are given on the input. The commits are __[here](https://github.com/common-workflow-language/gxargparse/commits/pypi2cwl)__, starting from June 26.

The second one is a tool with a purpose opposite to argparse2cwl - __[cwl2argparse](https://github.com/common-workflow-language/gxargparse)__. cwl2argparse allows parsing given CWL document(s) and generate a Python function which uses information about the tool and parameters to return an argparse `ArgumentParser` object. It allows to develop tools backward: write CWL definition first and then write language-specific implementation. Here is the history of commits for cwl2argparse: __[link](https://github.com/common-workflow-language/cwl2argparse/commits?author=anton-khodak)__


The last task was similar to what I've done with argparse2cwl - implementing the same functionality for [click](http://click.pocoo.org) argument parser. As a [small research](https://anton-khodak.github.io/argparse2cwl-blog/2016/05/16/argument-parsers.html) I've conducted at the beginning of GSoC showed, there is no single argument parser that is used in all bioinformatic tools. The most common are the ones from the standard libraries (argparse and sys.argv), but third-party parsers are also popular and require some attention. That's why it was decided to extend argparse2cwl to a more general *cmdline2cwl* interface and include *click* support. The code is represented by this __[pull request](https://github.com/common-workflow-language/gxargparse/pull/14)__.

To conclude, all of the tasks were accomplished in a required volume and on time, the original goals met and exceeded, so I consider GSoC as successfully completed. I hope the community will appreciate my work and contributions :) 


{% include disqus.html %}
