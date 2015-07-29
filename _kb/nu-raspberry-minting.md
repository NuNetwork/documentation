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
Holding NuShares comes with a responsibility : as a shareholder is in your best interest to participate to the network by submitting your votes in each mint you mint. 

To maximise the impact of your votes and the reward that comes with staking shares your Nu client should be minting 24/7.  A cost/efficient solution is delegating the minting to a cheap Raspberry Pi connected to the internet : unlike VPS or cloud service you will keep control over your shares, and you can finally turn off your home computer. 

The Raspberry Pi is a cheap (~40$) and efficient device with enough computational power to let you mint.   

In this minimal tutorial we will see how to setup a minting machine, not a [full node](https://bitcoin.org/en/full-node#other-linux-distributions). For security reasons full nodes and minting nodes should be kept separated. 

NOTE : in this tutorial we use pico as text editor, but feel free to use any other editor (nano,vi,etc). 

## What do you need
   - A Raspberry Pi [2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/)  ;
   - A fresh [SD card](https://www.raspberrypi.org/documentation/installation/sd-cards.md)  ;
   - An Ethernet cable or wifi dongle ;
   - Some [NuShares](https://nubits.com/nushares/introduction) (minimum 10k NSR are required for minting) ;
   - Basic CLI linux skills ;

## Prepare the Raspberry Pi
- Download and install NOOBS, an easy operating system installer which contains Raspbian following the [the official tutorial](https://www.raspberrypi.org/help/noobs-setup/);
- Update all existing software on the Pi 
`$ sudo apt-get update`
`$ sudo apt-get upgrade`
- Install dependencies required by Nu
`$ sudo apt-get install checkinstall subversion git git-core build-essential`
`$ sudo apt-get install libssl-dev libdb++-dev libminiupnpc-dev`
`$ sudo apt-get install libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libcurl4-openssl-dev`
- Link libminiupnpc 
`$ sudo ln -s /usr/lib/libminiupnpc.so.5 /usr/lib/libminiupnpc.so.10`

Additionally we suggest to follow the optional steps below for additional security : 

- Setup static ip for your raspberry following one of the many tutorials you can find online, for example [this](http://www.modmypi.com/blog/tutorial-how-to-give-your-raspberry-pi-a-static-ip-address);
- Enable SSH : enter `sudo raspi-config` in the terminal, then navigate to ssh, hit Enter and select `Enable or disable ssh server`.
- Configure your raspberry to accept passwordless SSH sessions [following this tutorial](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md) , or if you know what you are doing simply run `$ cat ~/.ssh/id_rsa.pub | ssh pi@<IP-ADDRESS> 'cat >> .ssh/authorized_keys' `
- Disable SSH password login  by editing /etc/ssh/sshd_config
`$ sudo pico /etc/ssh/sshd_config`
and making sure these three parameters are set to `no`
{% highlight text %}
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
{% endhighlight %}
Restart SSH with `$ sudo /etc/init.d/ssh restart`


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

- Avoid lovale problems with locale
`$ echo export LC_ALL=en_US.UTF-8 >> ~/.profile`

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
