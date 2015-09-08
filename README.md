# documentation

This repo contains the source for [docs.nubits.com] (http://docs.nubits.com). The page is generated directly from the source in this repo using [github pages] (https://pages.github.com/)

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/NuNetwork/documentation?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Contribute 

If you want to contribute to the documentation feel free to fork this repository and submit a PR.

Adding a new page is as easy as creating a new file under the *_kb* directory and filling it with proper metadata at the top of the file :


{% highlight text %}
---
title: <Explanatory title>
nav_heading: <the category of navbar - see _data/navigation.yml>
filename: <name-of-the-file.md>
permalink: <permalink to doc ( e.g. /accept-nubits/ )>
layout: kb
lang: en
callouts:
---
{% endhighlight %}



