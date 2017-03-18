---
layout: post
title:  "CWL week in London"
date:   2017-03-17 18:44:27 +0300
comments: true
---
After the successful completion of my GSoC projects, I was invited to meet my mentors Michael R. Crusoe and Roman Valls Guimera and attend CWL work session that took place in London from the 1st to the 4th November 2016. I was thrilled with this opportunity, and though it took quite a while for me to organize this journey (my first single voyage abroad), it was undoubtfully worth it. 

I arrived in London a little earlier to take part in [Mozilla Festival 2016](https://mozillafestival.org/) together with Roman. On the festival, I presented my summer projects to people from bioinformatics community who participated in Mozfest's [Open Science Fair](https://app.mozillafestival.org/#_space-open-science).

The CWL week started a day later. The attendees were me, Michael, Roman, Janko Simonovic and Ivan Batic from Seven Bridges Genomics, Niels Drost from the Netherlands eScience Center and <*sorry, I forgot the name of this gentleman, remind me, please, Michael*> from IBM. During these four days, I worked on polishing the tools I developed ([argparse2tool](https://github.com/erasche/argparse2tool), [pypi2cwl](https://github.com/common-workflow-language/pypi2cwl), [cwl2argparse](https://github.com/common-workflow-language/cwl2argparse)) on the basis of the feedback from all the participants. We explored the question of pip installability, filed a bunch of [issues](https://github.com/common-workflow-language/gxargparse/issues?utf8=%E2%9C%93&q=%20is%3Aissue%20), tried applying argparse2tool to [khmer](https://github.com/dib-lab/khmer) scripts. Another thing we tackled was fixing bugs with running [Toil](https://github.com/BD2KGenomics/toil) workflow engine on SLURM cluster. In addition, I learned about the inners of another important open-source implementation for CWL [bunny](https://github.com/rabix/bunny) directly from its creator Janko. During the CWL week, it was added to the community run continuous integration server and successfully [passed](https://twitter.com/commonwl/status/793767714049384448) latest conformance tests. 

Overall, it was a highly intensive and productive hackathon. I was very happy to meet my mentors and other people from the CWL community in person and to work with them for these few days. I could not imagine a better finish of my Google Summer of Code 2016 participation!

![Me with my mentors Michael R. Crusoe and Roman Valls Guimera][photo]
*That happy! :)*

[photo]: {{site.url}}/assets/london.jpg

P.S. A year after, I became a mentor on a CWL project myself! Check the idea here: [CWL reference implementation (cwltool) idea](https://obf.github.io/GSoC/ideas/#cwl-reference-implementation-cwltool).

P.P.S. Special thanks to [Open Bioinformatics Foundation](https://www.open-bio.org/wiki/Main_Page) for awarding me with the travel fellowship and reimbursing with that a significant part of my travel expenses.


{% include disqus.html %}
