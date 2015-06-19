---
title: Creating a conf file
nav_heading: Technical Resources
filename: creating-conf-file.md
permalink: /creating-conf-file/
layout: kb
lang: en
callouts:
    - shortname: line-comments
      type: info
      title: Adding comments to the conf file
      body: Lines that start with # are comments, and are ignored
    - shortname: hidden-dirs
      type: warning
      title: data directories are hidden by default
      body: Data directories are usually marked as hidden folders by default, meaning you will have to change some settings in order to see them. Please review the links below for your platform on how to enable viewing hidden folders.[Windows](http://www.howtogeek.com/howto/windows-vista/show-hidden-files-and-folders-in-windows-vista/)\n\n[Linux](http://www.howtogeek.com/howto/ubuntu/view-hidden-files-and-folders-in-ubuntu-file-browser/)\n\n[OSX](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/)"
---

#Creating a nu.conf file

Sometimes you may need to use a configuration file to change the behavior of the nu client. Learn how to locate your data directory, and create a conf file.

##1. Find the Nu data directory

First you'll need to find the Nu data directory. This directory location will be different depending on the operating system you're using. The table below can assist you in finding it.

{% include callout-block.html name="hidden-dirs" %}

```
Windows 8/7/2K8/Vista
    C:\Users\%USERNAME%\AppData\Roaming\nu
Windos XP/2K3/2K
    C:\Documents and Settings\%USERNAME%\Application Data\nu",
Linux
    ~/.nu
OSX
    ~/Library/Application Support/Nu
```


##2. Create a nu.conf file

After locating the nu folder in your data directory create a new file called nu.conf. Make sure to keep it all lowercase.

##3. Edit the nu.conf file

Now you can add commands to your conf file that will change the behavior of the wallet client and daemon when they are started. The sample file below shows you some common commands. For a list of other commands you can enter into the conf file visit the [Client Commands](http://nubits.readme.io/v1.0/docs/nu-client-commands) page.

##Make sure the file is being saved in plain text. If you accidentally saved the file in a format such as .doc or .rtf Nu will not be able to use it.


#Sample file

```
#Set a unique RPC username and password after the equal sign.
rpcusername=NuBitsUser
rpcpassword=NuBitsPassword
 
#Starts the RPC server so your client can accept RPC commands
server=1
 ```
{% include callout-block.html name="line-comments" %}
