---
title: Performing Backups
nav_heading: Getting Started
filename: performing-backups.md
permalink: /performing-backups/
layout: kb
lang: en
callouts:
  - shortname: multiple-units
    type: danger
    title: Each unit has its own wallet file
    body: Each unit has a separate wallet file. You must make sure to make separate backups for each unit. If you only backup your NuBits wallet, then you must still back up your NuShares wallet.

---

> Security is always excessive until it's not enough.

— Robbie Sinclair, Head of Security, Country Energy, NSW Australia

You should always reguarly backup your wallet files, and have multiple backups stored on various media and locations. It's also a good idea to backup your data directory prior to using newer wallet verions. Though many times you will be warned if this is a neccesary action. Here we'll go over the steps needed to perform different types of backups.

## Wallet backups

The safest way to backup your wallet files is by using the wallet itself.

{% include callout-block.html name="multiple-units "%}

### Using the GUI wallet (Desktop wallet):

 1. Click "File" at the top left
 1. Click "Backup Wallet"
 1. From here you can choose to save your wallet file and also give it a name.
 
 Remember to do this for all units (NuShares, NuBits, etc). You can see which unit you're backing up by clicking the "Unit" menu option. You can also change units from here as well to back up others.
 
### Using the Daemon

 1. Use the `backupwallet` command to backup the wallet from the daemon. Provide the location and file name as a parameter where you would like it to be backed up.
 1. `./nud backupwallet "/path/to/location/walletS.dat"`
 
 This command will backup your NuShares wallet by default. To back up other unit wallets you must supply the unit flag with the unit code. The example below shows how to backup your NuBits wallet.
 
 `./nud --unit=B backupwallet "/path/to/location/walletB.dat"`
 
 
 ## Using the Data Directory
 
 On some occasions you may not be able to start up the Nu application, so you'll be unable to backup your wallet files from it using the steps above. In those instances you can use the next best option which is to copy the wallet files from the data directory. **You should never do this while the Nu application is running. Always shut down Nu first**.
 
 1. First locate the data directory for your operating system. You can use the guide [located here](https://docs.nubits.com/creating-conf-file/#find-the-nu-data-directory).
 1. Inside the Nu data directory will be your wallet files. Their naming convention follows "wallet<unit>.dat". For instance the NuBits wallet will be "walletB.dat" and the NuShares wallet will be "walletS.dat". Copy all of your wallet files from this directory in order to back them up.  
 
 ## Data Directory Backup
 
 In some cases you'll want to back up your entire data directory which contains your wallet files, blockchain, and other data required by Nu to run. Follow the steps to create a backup of the data directory.
 

 
  1. First locate the data directory for your operating system.  You can use the guide [located here](https://docs.nubits.com/creating-conf-file/#find-the-nu-data-directory).
  1. If you need to keep the existing data directory simply copy/paste the entire directory somewhere. If you don't need to keep the files in place just rename the directory. For exanmple you can add "BACKUP" to the end, which on a Linux system would look like ".nuBACKUP". 
