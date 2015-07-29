---
title: Mminting on a Raspberry Pi
nav_heading: Technical Resources
filename: nu-raspberry-minting.md
permalink: /nu-raspberry-minting/
layout: kb
lang: en
callouts:
---

## Introduction
Why is important
What is minting
Minting vs full node


## What do you need
   - A Raspberry Pi [2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/) 
   - A fresh [SD card](https://www.raspberrypi.org/documentation/installation/sd-cards.md) 
   - An Ethernet cable or wifi dongle
   - Some [NuShares](https://nubits.com/nushares/introduction) (minimum 10k NSR are required for minting)

## Prepare the Raspberry Pi
Download Noobs
Format your SD card
Install Noobs (raspian)
Setup static ip
enable ssh keys  login
disable password login
`$ cat ~/.ssh/id_rsa.pub | ssh <USERNAME>@<IP-ADDRESS> 'cat >> .ssh/authorized_keys' `

`$ sudo pico /etc/ssh/sshd_config`
{% highlight text %}
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
{% endhighlight %}
`$ sudo /etc/init.d/ssh restart`

Avoid lovale problems with locale
`$ echo export LC_ALL=en_US.UTF-8 >> ~/.profile`

Update all existing software on the Pi (one line at a time)
`$ sudo apt-get update`
`$ sudo apt-get upgrade`

Install required dependencies
`$ sudo apt-get install checkinstall subversion git git-core build-essential`
`$ sudo apt-get install libssl-dev libdb++-dev libminiupnpc-dev`
`$ sudo apt-get install libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libcurl4-openssl-dev`

Link libminiupnpc 
`$ sudo ln -s /usr/lib/libminiupnpc.so.5 /usr/lib/libminiupnpc.so.10`


## Download and compile Nu
`$ cd ~`
`$ git clone https://bitbucket.org/JordanLeePeershares/nubit.git` 
`$ cd nubit/src` 
`$ sudo dd if=/dev/zero of=/swapfile bs=64M count=16` 
`$ sudo mkswap /swapfile` 
`$ sudo swapon /swapfile` 
`$ make -f makefile.unix` 
`$ strip nud` 
`$ mv nud ~`
`$ cd ~`
`$ sudo rm -r nubit/`
`$ sudo swapoff /swapfile`
`$ sudo rm /swapfile`
`$ sudo cp ~/nud /usr/bin/nud && sudo chmod a+x /usr/bin/nud`

## Configure Nu
`$  mkdir -p ~/.nu`
`$  touch ~/.nu/nu.conf`
`$  pico ~/.nu/nu.conf`

{% highlight text %}
daemon=1 
server=1
rpcuser=xxx
rpcpassword=yyy
port=7890
{% endhighlight %}

DO NOT Open ports

## Start Nud and download the blockchain
`$  nud -daemon`
`$  nud getinfo`

## Configure your minting machine

Configure to run as a service

reboot
Encrypt your wallet
Import private keys

Unlock wallet

pass (Type in the password to start minting. There is no prompt! the password shows! type password, press return, press control-D)
`$ nud walletpassphrase `cat` 999999999 true`


Check if is minting correctly

Configure datafeeds
https://docs.nubits.com/using-a-data-feed/#using-data-feeds-from-the-daemon

`$  nud setdatafeed https://raw.githubusercontent.com/Cybnate/NuNet-datafeed/master/Cybnate-datafeed.json https://raw.githubusercontent.com/Cybnate/NuNet-datafeed/master/Cybnate-datafeed.txt ShTrp9wbgnhZudk4eYXtBtcMyeBziGzUpc`

`$ nud getdatafeed `

Do stuff via RPC https://docs.nubits.com/rpc-api/

Use a GUI (also)
