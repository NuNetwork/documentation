---
title: Using a bootstrap file
nav_heading: NuBits
filename: bootstrap-file.md
permalink: /using-a-bootstrap/
layout: kb
lang: en
---

A bootstrap file allows you to download a large portion of the blockchain. The advantage is that the Nu wallet doesn't need to download the blocks from other peers. Syncing the blockchain from a boostrap file is much faster than downloading from peers. Follow the steps below to download and use a bootstrap file.

 1. Download the bootstrap.dat file [from here](https://docs.google.com/uc?id=0B96pmq-lU9NQTUlqYjY5S2xNNzQ&export=download). A [torrent file](https://bitbucket.org/JordanLeePeershares/nubit/downloads/NuBootstrap012616.torrent) is also available to download using bittorrent. 
 1. Place the bootstrap file into your Nu data directory. [You can follow this guide to find the data directory for your operating system](https://docs.nubits.com/creating-conf-file/#find-the-nu-data-directory).
 1. If you have Nu running already then restart it. If it's not running, go ahead and start it up.
 1. You should see at the bottom "importing blocks from disk". Your client is now syncing the blockchain using the bootstrap file.
 
The bootstrap file will never be 100% of the total blockchain, as it is always increasing. Once it has finished snycing with the available blocks from disk it will start to pull the most recent blocks from peers.

