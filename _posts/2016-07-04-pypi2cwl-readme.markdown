---
layout: post
title:  "pypi2cwl "
date:   2016-07-04 16:27:27 +0300
comments: true
---

`pypi2cwl` forms CWL tool descriptions from PyPi packages using `argparse2cwl`. It installs the package if it hasn't been installed before, downloads the source code to a new directory, parses command-line scripts from package's `setup.py` and runs `argparse2cwl` against those scripts. 

## Installing ##

`pypi2cwl` is installed as a part of `argparse2cwl`, refer to its [installation process](https://github.com/anton-khodak/argparse2cwl-blog/blob/27c649516d3cdb736cba7c312b9435074cbeb6d8/_posts/2016-06-20-alpha-release-notes.markdown).


## Usage ##

	$ pypi2cwl <package_name> [options]

Options (some of them are inherited from `argparse2cwl`):

* `-go`, `--generate_outputs`: flag for generating outputs not only from arguments that are instances of `argparse.FileType('w')`, but also from every argument which contains `output` keyword in its name. For instance, argument `--output-file` with no type will also be placed to output section. However, '--output-directory' argument will also be treated like File, so generated tools must be checked carefully if when this option is selected.


* `-d`, `--directory`: directory for storing tool descriptions.

* `-v`, `--venv`: this flag must be used if `pypi2cwl` is run inside a virtual environment. Then a package, if it wasn't installed before, will be installed locally. 

## Limitations ##

`pypi2cwl` cannot process packages where 
a) tools are not defined as command-line scripts in `setup.py`
b) argument parsers other than `argparse` (for instance, `sys.argv`) are used.

In these cases you should manually generate tool descriptions using `argparse2cwl`. 


{% include disqus.html %}

