---
title: Historical Data API
nav_heading: Nu Web Services
filename: historical-data-api.md
permalink: /historical-data-api/
layout: kb
lang: en
callouts:
  - shortname: beta
    type: warning
    title: Do not use beta software in production
    body: This API is a temporary beta and we advise not to use it in production environment. While we work towards a production-ready API, you can use this for toy projects and experiments.
  - shortname: timeframe
    type: info
    title: The Nu Network launched on September 24, 2014
    body: The first available data-points are dated 2014-10-17 12:05:58. The data format is reported as *json* raw data, as returned from the Nu daemon.
---
## Data API Introduction

{% include callout-block.html name="beta" %}

We have put together a temporary HTTP service to access historical data about the Nu Network.  A python script updates the database each time a new block is found, and updates the *getliquidityinfo* every 30 seconds.

{% include callout-block.html name="timeframe "%}

## Data API Overview

**Base URL** : http://nu.mj2p.co.uk/

**Parameters** : The API accepts three GET parameters:

Parameter Name | Description | Format
:--------------|:------------|:----------------
cmd | The name of the command to retrieve | See list <a href="#command">below</a>
frm | The date of the earliest record | `YYYY-MM-DD%20hh:mm:ss`
to  | The date you want to return data up to | `YYYY-MM-DD%20hh:mm:ss`

<div id="command"></div>

## List of Available Commands

  * `getinfo`
  * `getcustodianvotes`
  * `getdifficulty`
  * `getmotions`
  * `getparkrates`
  * `getpeerinfo`
  * `getrawmempool`
  * `getvote`
  * `getliquidityinfo`
  * `getparkvotes`

## API Usage Examples


Retrieve historical liquidity info specifying the time-range:
{% highlight bash %}
http://nu.mj2p.co.uk/nu-data?cmd=getliquidityinfo&frm=2014-10-18%2008:35:00&to=2014-10-18%2008:36:00
{% endhighlight %}

Retrieve historical *getpeerinfo* using smaller timestamps as 'frm' and 'to' :
{% highlight bash %}
http://nu.mj2p.co.uk/nu-data?cmd=getpeerinfo&frm=2014-10-18&to=2014-10-19
{% endhighlight %}

Retrieve all historical *getcustodianvotes* datapoints available
{% highlight bash %}
http://nu.mj2p.co.uk/nu-data?cmd=getcustodianvotes
{% endhighlight %}
