---
layout: post
title:  "Introduction to CWL generating tools"
date:   2016-08-11 09:15:27 +0300
comments: true
---
This post is an overview and quick start for the tools that were developed in this GSoC 2016 project. All the subprojects are aimed to spread [Common Workflow Language](commonwl.org) more widely in the developer community by making porting Python tools to CWL easier, with less amount of routine job. 

## [gxargparse](https://github.com/common-workflow-language/gxargparse)
*gxargparse* is a tool the original purpose of which was to form [Galaxy XML](https://wiki.galaxyproject.org/Admin/Tools/ToolConfigSyntax) tools from Python tools that use `argparse`. The design of the argparse translator was adapted to create the following converters (both of them are installed along with gxargparse)

# argparse2cwl

*argparse2cwl* allows to generate CWL tools out of Python tools with argparse as their argument parser. It works like a wrapper around the original argparse, capturing its arguments and using them to generate CWL tools when the tool is run with `--generate_cwl_tool` option. Basically, it looks like you are calling this tool without any parameters, just a command with some argparse2cwl options.

For instance, you have a tool named [search.py](https://github.com/common-workflow-language/common-workflow-language/blob/0c3e2c58de65961f225982041efd7c9baabc1dad/v1.0/v1.0/search.py). 

	#!/usr/bin/env python

	import argparse 

	parser = argparse.ArgumentParser(description="Toy program to search inverted index and "
		                                     "print out each line the term appears")

	parser.add_argument('mainfile', type=argparse.FileType('r'), help='Text file to be indexed')
	parser.add_argument('term', type=str, help='Term for search')

	args = parser.parse_args()

	# Here goes the code that works with argument values	
	pass

You import argparse and write your tool as normally, but argparse2cwl grabs all the information available from the code and uses it to generate a CWL tool. If you run

	python search.py --generate_cwl_tool

or 

	./search.py --generate_cwl_tool

The program will generate the next CWL file

	#!/usr/bin/env cwl-runner
	# This tool description was generated automatically by argparse2cwl ver. 0.3.0
	# To generate again: $ ./search.py -b ./search.py --generate_cwl_tool
	# Help: $ ./search.py  --help_arg2cwl

	cwlVersion: "cwl:v1.0"

	class: CommandLineTool
	baseCommand: ['./search.py']

	doc: |
	  Toy program to search inverted index and print out each line the term appears

	inputs:
	  
	  mainfile:
	    type: File
	  
	    doc: Text file to be indexed
	    inputBinding:
	      position: 1

	  term:
	    type: string
	  
	    doc: Term for search
	    inputBinding:
	      position: 2


	outputs:
	    [] 

and you just need to look through the document and add the information that couldn't be extracted from the code (requirements, hints, labels). Pay attention to the output section, it often can be blank because argparse2cwl couldn't recognize that a parameter belongs to output. Use `--generate-outputs` option to generate output parameters from the ones which have `output` keyword in their names. Other options more detailed in the [README](https://github.com/common-workflow-language/gxargparse/blob/cwl-refactor/README.md).


If you have a command with nested subcommands, `argparse2cwl` will discover them all and generate a bunch of tools for each subcommand. It is especially handy for bioinformatics toolkits which usually have one root command.    

#	 click2cwl

*click2cwl* shares absolutely the same logic as argparse2cwl, the only difference is it is adjusted to work with [click](http://click.pocoo.org/) argument parser. Whenever click is imported, gxargparse grabs its commands, arguments, options and forms CWL parameters out of them. 


## [pypi2cwl](https://github.com/common-workflow-language/pypi2cwl/)

*pypi2cwl* is a small wrapper around argparse2cwl that goes further in its desire to facilitate tool wrapping. After running 
   
	pypi2cwl <PYPI-PACKAGE>

it

1. Installs `PYPI-PACKAGE` if it hasn't been installed before

2. Downloads the source code to a new directory

3. Checks for command-line scripts in its `setup.py`.

4. Runs argparse2cwl against them and generates the associated CWL output files.

pypi2cwl is available over `pip`.

## [cwl2argparse](https://github.com/common-workflow-language/cwl2argparse/)

*cwl2argparse* does the job straightly opposite to what argparse2cwl does: it parses CWL tools and generates Python code which can be imported as a function and used. It looks like this: supposing there is a file named `search.cwl`


    #!/usr/bin/env cwl-runner
    cwlVersion: "cwl:draft-3"
    class: CommandLineTool
    baseCommand: ['search.py']
    
    description: |
      Toy program to search inverted index and print out each line the term appears
    inputs:
      - id: mainfile
      type: File
      description: Text file to be indexed
      inputBinding:
        position: 1
    
    - id: term
      type: string
      description: Term for search
      inputBinding:
        position: 2
    
    outputs:
        []

Running `cwl2argparse search.cwl` generates the following file:


    import argparse
    
    
    def parser():
        description="""
            Toy program to search inverted index and print out each line the term appears
        """
        
        parser = argparse.ArgumentParser(description=description)
        arg_mainfile = parser.add_argument("arg_mainfile",
            type=argparse.FileType(),       help="""Text file to be indexed""",)
        arg_term = parser.add_argument("arg_term",
            type=str,       help="""Term for search""",)
    
        return parser


cwl2argparse is also installed by `pip`.


That's all I've been working on during GSoC 2016 :) I will support the projects after their release, if confronted with any problems, please open issues, report bugs, I will fix them as soon as possible.

{% include disqus.html %}
