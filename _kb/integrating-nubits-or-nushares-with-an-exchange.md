---
title: Integrating With An Exchange
nav_heading: Technical Resources
filename: integrating-nubits-or-nushares-with-an-exchange.md
permalink: /integrating-nubits-or-nushares-with-an-exchange/
layout: kb
lang: en
callouts:
    - shortname: use-avatar
      type: danger
      title: You must add avatar=0 if you're using NuShares
      body: If you are configuring NuShares you MUST add ```avatar=0``` to your conf file\n\n```\nrpcuser=anyusername\nrpcpassword=anypassword\nserver=1\navatar=0\n```"
---


This guide will explain how you can integrate NuBits and NuShares into your exchange.

##1. Download the daemon"

From [NuBits.com/download](http://nubits.com/download) you can find a package containing the daemon for your environment. The daemon will be called "nud" or "nud.exe" depending on your platform.

##2. Create a nu.conf file"

Before running the daemon you will need to create a nu.conf file. Follow our [creating a nu.conf file](hooow do I link to this) guide to learn how to create the file. Place the following into your file:

```
rpcuser=anyusername
rpcpassword=anypassword
server=1
```
{% include callout-block.html name="use-avatar" %}

##3. Start the daemon"

Run the daemon using the --daemon parameter

Ex.``` ./nud --daemon```

This will start the daemon in the background and begin syncing the blockchain. Run ``` ./nud getinfo``` to verify you can communicate with the daemon through RPC.

###4. Point your exchange software to the correct daemon unit"

Nu uses different port numbers for different units. The only units in the software right now are NuBits and NuShares, but this may change in the future. Use the following guide below to select the port number for the unit you're configuring.

```
PROTOCOL PORT 7890
// Base RPC port used by the NuShares RPC server.
// Other unit RPC servers listen on RPC_PORT+1, RPC_PORT+2, etc.
RPC PORT 14001     // NuShares
RPC PORT 14002     // NuBits

// Same rules apply to testnet, but on different ports
TESTNET PORT 7895
TESTNET RPC PORT 15001     // NuShares
TESTNET RPC PORT 15002     // NuBits

// Peercoin ports used when communicating with the Peercoin wallet for dividend distributions
PEERCOIN RPC PORT 9902
PEERCOIN TESTNET RPC PORT 9904
```

Have your software point to the correct port number to interface with the unit you're configuring. For example this is how we would communicate with the NuBits unit in the Peatio exchange software

``` "rpc: http://nuEx:123exch@127.0.0.1:14002"; ```
