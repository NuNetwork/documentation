---
title: Using A Data Feed
nav_heading: NuShares
filename: using-a-data-feed.md
permalink: /using-a-data-feed/
layout: kb
lang: en
callouts:
---
## About data feeds

Data feeds let users configure their Nu client to pull voting data from the internet. All that is needed is a URL to the voting data. You can use the **setdatafeed** RPC call to configure the feed from the command line. The **getdatafeed** RPC can be used to view the current feed. The client pulls the data every 60 seconds by default, but this can be changed using the **datafeeddelay** configuration (for example you can add `datafeeddelay=30` in your nu.conf). The data feed information is stored in your NuShares wallet.dat file.

Your previous votes in the client are replaced when you set a data feed. If votes are manually added after you set the feed they will be removed on the next pull. You optionally can choose to ignore individual parts of a voting feed (motions, custodians, or park rates). If you choose to ignore custodian votes from the feed, for example, you may manually edit custodian votes in the client without the data feed overwriting them. All parts are selected by default.

## Adding a data feed

The data feed button can be found at the bottom of the NuShares voting page

{% include image.html filename="nushares_wallet_overview_page.png" caption="NuShares wallet overview" %}

Pressing the data feed button will open up the feed dialog box. From here you can provide the data feed URL, and select which parts of the voting data you would like your client to pull down.

{% include image.html filename="data_feed_dialog.png" caption="Data feed dialog" %}

## URL Signature

In the screen shot above you'll notice two extra fields. To prevent man-in-the-middle attacks data feed sources may also provide a secondary URL that points to a signature of the voting data. They will also provide the NuShares address used to sign it. These two additional pieces of information can help assure that votes have not changed while traveling to the client. The client will display an error if a change has been noticed and the feed data will be ignored. The URL signature is not required to use data feeds, but it is much more secure.

## votenotify Configuration

It’s still very important for users to be aware of what they’re voting for when using a feed. The vote data provided by the data feed is always recorded in debug.log (but the file is truncated regularly). In addition the **votenotify** configuration is available. Providing this configuration the path to a script in the [nu.conf file]({{ site.url }}{{ site.baseurl}}/creating-conf-file) will invoke that script when votes are changed. This could be used to trigger a script that sends an email, or creates a file with a diff of the changes for review.

{% gist 6bd15ce07fb51b962938 %}

## Using data feeds from the daemon

Setting the data feed:
{% highlight bash %}
nud setdatafeed https://abc.com/my-datafeed.json
{% endhighlight %}

Setting up a signed data feed:
{% highlight bash %}
nud setdatafeed https://abc.com/my-datafeed.json https://abc.com/my-datafeed.json.signature SSPwKhtFEyQvUx9cPjaC8yUxdeNrTMfJfF
{% endhighlight %}

Using only specific parts of a data feed (custodians, park rates, motions):
{% highlight bash %}
nud setdatafeed https://abc.com/my-datafeed.json https://abc.com/my-datafeed.json.signature SSPwKhtFEyQvUx9cPjaC8yUxdeNrTMfJfF custodians,parkrates
{% endhighlight %}

Or without signature:
{% highlight bash %}
nud setdatafeed https://abc.com/my-datafeed.json "" "" custodians,parkrates
{% endhighlight %}

To verify your current settings:
{% highlight bash %}
nud getdatafeed
{% endhighlight %}
