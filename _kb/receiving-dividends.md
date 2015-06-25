---
title: Receiving Dividends
nav_heading: NuShares
filename: receiving-dividends.md
permalink: /receiving-dividends/
layout: kb
lang: en
callouts:
---

## Instructions for how to set up your connection between Peer(coin/unity) and Nu

Dividends are sent out in the form of Peercoins. Once you export the Peercoin keys from your Nu wallet into your Peer(coin/unity) wallet the dividends will be accessible. Follow the instructions below to export the keys.

Make sure that for both Nu and your Peer(coin/unity) wallet client that you have a [configuration file]({{ site.url }}{{ site.baseurl }}/creating-conf-file) available, and that each has at a minimum the following information.

{% highlight bash linenos %}
server=1  
rpcuser={anything}  
rpcpassword={anything}  

#for use on the testnet, include `testnet=1`
{% endhighlight %}

* Once the configuration files are in place, launch both clients.
* Go back to your Nu wallet and change your units to work from the NuShares side (file menu: Unit > NuShares).
* From the file menu: Shares > Export Peercoin keys

If everything works as expected, you will see a dialog appear with a count of the number of addresses that have been exported. You can confirm this action by viewing your Peercoin wallet and looking on the "Receive Coins" tab. There should be a number of new addresses with the label "NuShares" that match the number that was exported in the previous step. If you do not see this, please make sure that your wallet was unlocked (and not just unlocked for minting) and try it again.

{% include image.html filename="nushares_export_keys.png" caption="NuShares export keys dialog" %}

In your Peercoin wallet client, on the Receiving tab, you will see that the NuShares dividend addresses have been included:

{% include image.html filename="peercoin_exported_keys_view.png" caption="NuShares export keys" %}

Once that has been completed, you'll be ready for a dividend distribution. If you should add additional NuShares addresses in the future, please make sure you follow the same steps again to integrate those new paired keys into your Peercoin wallet. You will not duplicate existing keys, so this operation can be run as many times as you need, into the future.

## Troubleshooting

### 0 key(s) were exported to Peercoin

If you see a dialog like this, when you try to export the keys:

{% include image.html filename="nushares_export_keys_troubleshooting.png" caption="NuShares export keys troubleshooting" %}

You have probably already exported the keys to your client. Check your Peer(coin/unity) client to see if the keys exist.

### Port conflicts

If you experience problems with connecting the two wallets, please confirm that your network allows traffic on the following ports:

{% highlight bash %}
PROTOCOL PORT  7890
RPC PORT  14001     // Base RPC port used by the NuShares RPC server. Other unit RPC servers listen on RPC_PORT+1, RPC_PORT+2, etc.
RPC PORT  14002     // NuBits

// Same rules apply to testnet, but on different ports
TESTNET PORT   7895
TESTNET RPC PORT  15001     // NuShares
TESTNET RPC PORT  15002     // NuBits

// Peercoin ports used when communicating with the Peercoin wallet for dividend distributions
PEERCOIN RPC PORT  9902
PEERCOIN TESTNET RPC PORT  9904
{% endhighlight %}
