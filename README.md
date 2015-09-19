# documentation

This repo contains the source for [docs.nubits.com] (http://docs.nubits.com). The page is generated directly from the source in this repo using [github pages] (https://pages.github.com/)

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/NuNetwork/documentation?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Contribute 

If you want to contribute to the documentation feel free to fork this repository and submit a PR.

Adding a new page is as easy as creating a new file under the *_kb* directory and filling it with proper metadata at the top of the file :

```
---
title: <Explanatory title>
nav_heading: <the category of navbar - see _data/navigation.yml>
filename: <name-of-the-file.md>
permalink: <permalink to doc ( e.g. /accept-nubits/ )>
layout: kb
lang: en
callouts:
---
```

You can see an example of the raw text for the front page of docs.nubits.com [here](https://raw.githubusercontent.com/NuNetwork/documentation/gh-pages/_kb/getting-started-with-nu.md)


### callouts

Callouts can draw the users attention to important information. Adding a callout first requires to add callout metadata to the top of the page. You can see an example of two callouts described below.

```
callouts:
  - shortname: hidden-dirs
    type: warning
    title: Data directories are hidden by default
    body: | # this means to ignore newlines until "- shortname:"
      Data directories are usually marked as hidden folders by default, meaning you will have to change some settings in order to see them. Please review the links below for your platform on how to enable viewing hidden folders.

      - [Windows](http://www.howtogeek.com/howto/windows-vista/show-hidden-files-and-folders-in-windows-vista/)  
      - [Linux](http://www.howtogeek.com/howto/ubuntu/view-hidden-files-and-folders-in-ubuntu-file-browser/)  
      - [OSX](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/)
  - shortname: line-comments
    type: info
    title: Adding comments to the conf file
    body: Lines that start with \# are comments, and are ignored
```

Note the spacing, as this is important when descriing callouts. Once a callout has been described in the metadata youc can add it into the body of the document using the code below.

`{% include callout-block.html name="hidden-dirs" %}`

This code will be replaced with the callout box when the page is rendered. Notice that the `name` field must be the same as the `shortname` field in the callout metadata. There are three kinds of callouts. Info, warning, and danger, which are differentiated by different icons and colors.

![danger callout](https://raw.githubusercontent.com/NuNetwork/documentation/gh-pages/assets/images/danger_callout_example.PNG)
![info callout](https://raw.githubusercontent.com/NuNetwork/documentation/gh-pages/assets/images/info_callout_example.PNG)
![warning callout](https://raw.githubusercontent.com/NuNetwork/documentation/gh-pages/assets/images/warning_callout_example.PNG)
