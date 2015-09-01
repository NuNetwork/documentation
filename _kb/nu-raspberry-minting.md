---
title: Minting on a Raspberry Pi
nav_heading: Technical Resources
filename: nu-raspberry-minting.md
permalink: /nu-raspberry-minting/
layout: kb
lang: en
callouts:
---

## Introduction
Holding NuShares comes with a responsibility : it is in your best interest to participate to the network by submitting your votes in each block you mint. 

To maximise the impact of your votes and the reward that comes with staking shares, your Nu client should be minting 24/7.  A cost-efficient solution is delegating the minting to a cheap Raspberry Pi connected to the internet : unlike VPS or cloud service you will keep control over your shares, and you can finally turn off your home computer.  Thanks to  [Nu data-feeds](https://docs.nubits.com/using-a-data-feed/), you can subscribe your raspberry to an external source and control your votes without need to access the pi all the time. 

The Raspberry Pi is a cheap (~40$) and efficient device with enough computational power to let you mint.   

In this minimal tutorial we will see how to setup a minting machine which is different from a [full node](https://bitcoin.org/en/full-node#other-linux-distributions). For security reasons full nodes and minting nodes should be kept separated. 

NOTE : in the examples of this tutorial we used `pico` as text editor, but feel free to use any other editor (nano, vi, etc ...) . 

## What you need
   - A Raspberry Pi [2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/). The  1B and 1B+ can also be used to mint, although R-pi 2 is more efficient, especially when minting with a large number of shares. 
   - A fresh [SD card](https://www.raspberrypi.org/documentation/installation/sd-cards.md), ideally 8+ GB, class 10 speed  ;
   - An Ethernet cable or a WiFi dongle ;
   - Some [NuShares](https://nubits.com/nushares/introduction) (minimum 10k NSR are required for minting) ;
   - Basic [unix CLI skills](http://linuxcommand.org/) ;

## Prepare the Raspberry Pi

#### Download and install NOOBS
Follow the [the official tutorial](https://www.raspberrypi.org/help/noobs-setup/) to install an easy operating system installer which contains Raspbian. Login with your `pi` user, and [connect the raspberry to the internet](https://learn.adafruit.com/downloads/pdf/adafruits-raspberry-pi-lesson-3-network-setup.pdf). 

#### Update all existing software on the Pi 
 - `$ sudo apt-get update`
 - `$ sudo apt-get upgrade`

####  Setup static ip 

Following one of the many tutorials you can find online, for example [this](http://www.modmypi.com/blog/tutorial-how-to-give-your-raspberry-pi-a-static-ip-address);

#### Enable SSH : 
Enter `$ sudo raspi-config` in the terminal, then navigate to ssh, hit Enter and select `Enable or disable ssh server`.
#### Accept passwordless SSH sessions 
[Follow this tutorial](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md), or if you know what you are doing simply run (on your machines) 

- `$ cat ~/.ssh/id_rsa.pub | ssh pi@<IP-ADDRESS> 'cat >> .ssh/authorized_keys' `

#### Disable SSH password login 
Edit `/etc/ssh/sshd_config`

- `$ sudo pico /etc/ssh/sshd_config`

and make sure these three parameters are set to `no`

{% highlight text %}
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
{% endhighlight %}

Restart SSH with `$ sudo /etc/init.d/ssh restart`

#### Install dependencies required by Nu
 - `$ sudo apt-get install checkinstall subversion git git-core build-essential`
 - `$ sudo apt-get install libssl-dev libdb++-dev libminiupnpc-dev`
 - `$ sudo apt-get install libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libcurl4-openssl-dev`
 - 
#### Link libminiupnpc 

 - `$ sudo ln -s /usr/lib/libminiupnpc.so.5 /usr/lib/libminiupnpc.so.10`

## Compile Nu from sources
The build process can take long. If you want to skip it and get precompiled binaries instead, skip this section and go to the next.

 - `$ cd ~` #Go to pi user's home directory
 - `$ git clone https://bitbucket.org/JordanLeePeershares/nubit.git`   #clone NuBits repository locally
 - `$ cd nubit/src` #Go to source directory 
 - `$ sudo dd if=/dev/zero of=/swapfile bs=64M count=16` #provide some extra swap partition to speed up compilation time
 - `$ sudo mkswap /swapfile` 
 - `$ sudo swapon /swapfile` 
 - `$ make -f makefile.unix` #Build  nud. This command can take up to 2 hours, will produce an executable file : `nud`
 - `$ strip nud` #Reduce file size by stripping symbols
 - `$ sudo mv nud /usr/bin/nud && sudo chmod a+x /usr/bin/nud` #move nud and make it executable
 - `$ sudo rm -r ~/nubit/` #Remove directory with sources (optional)
 - `$ sudo swapoff /swapfile`#clean up the previously initiated swap
 - `$ sudo rm /swapfile`

## Download precompiled binaries 

You can download unofficial precompiled build maintaned by the Nu community. Read the disclaimer on [this repository](https://github.com/desrever-nu/nu-raspberry-unofficial) and download nud : 
- `$ sudo wget https://github.com/desrever-nu/nu-raspberry-unofficial/raw/master/latest/nud `
- `$ sudo mv nud /usr/bin/nud && sudo chmod a+x /usr/bin/nud` #move nud and make it executable


## Configure Nud

Now that nud is ready, we need to configure it before executing it. 

- `$  mkdir -p ~/.nu`#Create the data folder 
- `$  touch ~/.nu/nu.conf` #Create an empty configuration file
- `$  pico ~/.nu/nu.conf`#Edit the nu.conf file

Your nu.conf shuold look like the example below : 

{% highlight text %}
daemon=1 
server=1
rpcuser=<chooseAnUsername>
rpcpassword=<chooseAPassword>
port=7890
{% endhighlight %}

After editing the config, make it read only : 
 - `$ sudo chmod 400 ~/.nu/nu.conf`
 
The  nu daemon will be listening to RPC messages on the port you specified. We highly suggest *not* to forward that port and leave the pi protected behing the NAT, for local usage only.  

## Start Nud and download the blockchain

Now you will be able to access nud via CLI by typing `nud` followed by the [rpc command](https://docs.nubits.com/rpc-api/) you want to invoke.  
The first thing you want to do is starting the daemon and let it download the blockchain. This operation can take  several hours - or even days - depending on connectivity.  

- `$  nud -daemon` #will start your nu daemon , startup can take some minutes. 

It is possible that you get an error related to perl and your `locale` settings.  If you get this  error, simply execute the following command that will write an export of your locale to the bash profile your `locale` setting (in the example below being `en_US,` but could also be `en_GB`or something else). 
- `$ echo export LC_ALL=en_US.UTF-8 >> ~/.profile`

To check how the download of the blockchain is proceeding you can run 

- `$  nud getinfo`

and read the `blocks` number growing while comparing it to the current `height` on [the block explorer](https://blockexplorer.nu/status).   Be patient while the blockchain is being downloaded.

## Configure your minting machine

You can configure nud to automatically run on startup. 
 - `$ sudo pico /etc/rc.local`
and add the following line immediately before the last line (`exit 0`) : 
{% highlight text %}
.
.
.
nud -daemon
exit 0
{% endhighlight %}

Save, exit pico and reboot the pi with

- `$  sudo reboot`

and test if the daemon started automatically : 

- `$  nud getinfo`

### Fund your minting machine. 

You have three options to transfer NuShares to your raspberry : 

1. Send NSR to one of the raspberry receive address (list available receive address with `$ nud listreceivedbyaddress 1 true`
2. Import an existing private key using `$ nud importprivkey <yourprivkey>`  and clean up bash history right after with `$ cat /dev/null > ~/.bash_history` to delete all traces
3. Copy an existing walletS.dat file to the raspberry using `scp` . Execute this command from the machine where the existing wallet is hosted :  
`$ scp local/path/to/walletS.dat pi@<pi.ip.address>:/home/pi/.nu `

Unless you go with the the third option and imported an encrypted wallet, make sure to **encrypt your wallet** with a [sufficiently complex passphrase](https://answers.uchicago.edu/16276) 
- `$ nud encryptwallet <passphrase>` 

After you have a working node encrypted and funded with NuShares,  you need to **unlock the wallet** using your passphrase to allow minting. 
To unlock your wallet, type the command below, press enter,  then type your passphrase,  press enter again and finally Control+D:

```
$ nud walletpassphrase `cat` 999999999 true
```
Alternatively, you can use [this bash script](https://gist.github.com/desrever-nu/6e18d037251edeaeb4d6) so you don't have to remember the sequence above everytime. 

### Configure votes

Now you can use data-feeds to configure your vote, so everytime you mint a new block, you will participate to Nu democratic process.  You have also the option to manually configure votes via CLI, but is not reccomended.   

After you [created your own datafeed](https://docs.nubits.com/hosting-a-data-feed/) or chose an [existing datafeed](https://discuss.nubits.com/c/nushares/data-feeds) to delegate your voting power to, [this tutorial](https://docs.nubits.com/using-a-data-feed/#using-data-feeds-from-the-daemon) will teach you how to use data feeds from the daemon.  For example, to subscribe to [Cybnate's data feed](https://discuss.nubits.com/t/cybnates-datafeed-beta/1310) you can use the following command :

- `$  nud setdatafeed https://raw.githubusercontent.com/Cybnate/NuNet-datafeed/master/Cybnate-datafeed.json https://raw.githubusercontent.com/Cybnate/NuNet-datafeed/master/Cybnate-datafeed.txt ShTrp9wbgnhZudk4eYXtBtcMyeBziGzUpc`

Double check if the feed is set correctly by running 

- `$ nud getdatafeed `

Congrats, your minting machine is ready! 

 You can now interact with your node using [rpc commands](https://docs.nubits.com/rpc-api/), and you can also manage the same NSR with a GUI client from your laptop at the same time, just remember to leave the GUI client locked, so it won't mint and interfere with the raspberry.  
