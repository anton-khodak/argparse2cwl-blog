---
layout: post
title:  "argparse2cwl alpha release notes"
date:   2016-06-20 02:27:27 +0300
comments: true
---

`argparse2cwl` forms CWL tool descriptions from programs which use `argparse` as their argument parser. 

## Prerequisites ##
`argparse2cwl` is compatible with both Python 2 & 3.
Dependencies:
* Jinja2 >= 2.8

## Installing ##

Installation process:

1. Clone the source repository:
```$ git clone https://github.com/common-workflow-language/gxargparse.git ```  

2. Change directory to the root folder of the project and switch to `cwl-refactor` branch:
```$ git checkout origin/cwl-refactor```

3. Run 
```
   $ python setup.py install
   $ gxargparse_check_path 
```

## Running ##

To run `argparse2cwl`, call your tool as usually without actual arguments with `--generate_cwl_tool` option:
```$  



{% include disqus.html %}

