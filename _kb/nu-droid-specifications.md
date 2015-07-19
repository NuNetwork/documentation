---
title: NuDroid Specifications
nav_heading: NuDroid
filename: nu-droid-specifications.md
permalink: /nudroid/
layout: kb
lang: en
callouts:
---
## Release notes

**Release notes NuDroid v3.1:**

-	Issue with some of the Bitcoin QR codes fixed

**Release notes NuDroid v3.0:**

-   Shapeshift functionality
-	Store foreign coin addresses in address book
-	Scanning QR codes of other coins including Bitcoin
-	Export transactions to comma delimited file (CSV)
-	Improved peer recognition (faster synchronisation)
-	Bug fix causing crashes or payments not progressing.


Bonus functionality:

> -	Added an "Export" item in the menu on the main activity (transaction list) which exports the transaction details into a CSV file with the columns: Date, Label, In Amount, Out Amount (inc. fee), Fee, Address, Transaction Hash, Confirmations.
>-	Improved speed of finding peers.
>-	Bug fixes (e.g. wallet crashing fixed with Android 5.x and higher)


Limitations NuDroid v3.x with Bitcoin and altcoins

Bluetooth and NFC limitations of the Shapeshift technology:

When requesting a non-NuBits payment with Bluetooth enabled, the NuDroid app will not allow one to send via Bluetooth, but you can initiate a regular Shapeshift transfer. When using [BIP0070](https://bitcoinj.github.io/payment-protocol), the NuDroid app will try recognise the input, as it does not follow BIP0021 URIs. In this case BIP0070 should not be used when requesting Shapeshift payment from those using NuDroid. NFC using other apps will not work. To clarify what will work:

1.	Manually inputting address
2.	QR code of address
3.	QR code of BIP0021 URIs
4.	BIP0021 URI links

Coin support for Shapeshift functionality as of June 2015:

The NuDroid wallet v3.x supports the following coins:
Bitcoin, Blackcoin, BitcoinDark, Clams, Counterparty, Dash, Digibyte, Dogecoin, Feathercoin, Gemz, Litecoin, Mastercoin, Mintcoin, Namecoin, Novacoin, Potcoin, Peercoin, Quark, Reddcoin, Shadowcash, Startcoin, Storjcoin X, Swarm, Tether, Unobtanium, Vericoin

Currently not supported are:

Next, BitShares, Monero
This due to different address types being incompatible with NuDroid.

**Release notes v2.0**

The following functionality is included in the v2.0 release:

-	Deterministic wallets (BIP0032) or HD wallets 
-	New deterministic wallets mean that a wallet can be restored by a single backup.
-	Encrypt wallet with PIN code, required to send coins (under Safety, select spending PIN)
-	Displaying local currency in App widget User
-	Interface improvements 
-	Bug fixes and performance enhancements
-	Allows you to send fast Bluetooth payments by default.
-	New loading screens prevent "Application Not Responding" problems.

**Release notes 1.0**

The following functionality is included in the v1.0 Release:

- Private keys are stored on device and never shared
- Wallet backups
- Fast and secure centralised validation necessary for Proof-of-stake
- Simple transfer of coins using QR codes, NFC or URI links
- Widget displays balance and allows quick access to app functions
- Approximated currency conversions

## Shapeshift technology

**NuDroid powered by Shapeshift**
Depending on the liquidity available, coins can be unavailable at Shapeshift.io. New coins supported by Shapeshift.io from today on, won't be supported automatically. This requires an update of the App. 

The shapeshift service is delivered by Shapeshift.io. No sign-up is needed but a small fee does apply. More information can be found [here](https://shapeshift.zendesk.com/hc/en-us/articles/202585602-What-s-your-fee-structure-).  On top of that usual miner or network fees also apply depending on the coins used. To date (June 2015) transactions up to 1000 NBT are supported by Shapeshift. There is no guarantee though and it may fluctuate daily. 

## NFC (Near field communication) technology support

**Preparing and using tags**
The NuDroid wallet supports reading NuBits requests via NFC, either from a passive NFC tag or from another NFC capable Android device that is requesting coins.
For this to work, just enable NFC in your phone and hold your phone to the tag or device (with the "Request coins" dialog open). The "Send coins" dialog will open with fields populated.
Instructions for preparing an NFC tag with your address:

-	We have successfully tested this [NFC tag writer](https://play.google.com/store/apps/details?id=com.nxp.nfc.tagwriter). Other writers should work as well, let us know if you succeed.
-	Some tags have less than 50 bytes capacity, those won't work. 1 KB tags recommended.
-	The tag needs to contain a Nubits URI. You can construct one with the "Request coins" dialog, then share with messaging or email. You can also construct the URI manually. Example for Mainnet: nu:BG2Y2jP5YFZ5RGk2PXaeWwbeA5y1ZtFhoL
-	The type of the message needs to be URI or URL (not Text).
-	If you put your tag at a public place, don't forget to enable write protect. Otherwise, someone could overwrite the tag with his own Nubits address.

## Application Architecture

Andreas Schildbach architecture
The current codebase of NuDroid v3.x is based on the Andreas Schildbach Android Bitcoin wallet version 4.13. The Bitcoin wallet is at 4.32 as of June 2015. Here is the [list of changes](https://github.com/schildbach/bitcoin-wallet/compare/v4.13...v4.32) made since.
. This code may or may not be added in future official versions of NuDroid. However users can create their own unofficial builds if they wish.

NuDroid is a standalone NuBits node with no centralized backend required. NuDroid version 3.x has been coded to use the server at svr1.nubitsexplorer.nu. In version 4.x the user will be able to select one through an interface and with that NuDroid can be made completely trustless assuming the user runs their own instance of Abe explorer (svr1.nubitsexplorer.nu).

## Licensing and source code

GPL version 3
The NuDroid application is licensed under the GPL version 3. There is no warranty and no party shall be made liable to you for damages. If you lose coins due to this app, no compensation will be given. Use this App and the embedded Shapeshift services solely at your own risk.
-   The repository for the ABE explorer lives [here](https://github.com/Cybnate/NuBits-Abe-explorer). 
-   The repository for nubitsj lives [here](https://github.com/Cybnate/NuBitsj)
-   And the code for the wallet itself lives [here](https://github.com/Cybnate/NuDroid)

Pull request against these repositories will be considered on a case by case bases. Obtaining community support on discuss.nubits.com will greatly improve your chances.

## Wish list

The following is a wish list created based on community feedback, developers’ thoughts and logical next steps to further develop the App. There are no guarantees that one or any of the items on this list will be ever implemented in the official build beyond just an intention to continue to build and maintain this App. Please feel free to contribute to the discussion on discuss.nubits.com to have functionality added or deleted from this list and eventually implemented.

**Shapeshift related:**

-	Adding support to receive Bitcoin and other altcoins via Shapeshift and ability to display foreign QR codes to receive payments
-	Option to add email address to get receipt of transaction from Shapeshift by email
-	Provide a return address for each coin in case the transaction couldn't complete
-	Adding support for BKS exchange assuming they deliver a similar API as Shapeshift
-	Adding support for NXT, Monero and Bitshares and others Shapeshift has yet to add.

**Other:**

-	Synchronising codebase with Bitcoin App
-	Adding ability to set up recurring fixed payments (e.g. for donations, subscriptions, salaries)
-	Adding ability to import a series of transactions in a comma delimited file format for immediate payments
-	User interface for using multi-sig addresses
-	User interface to switch between main and test network
-	Integrating [OpenAlias](https://discuss.nubits.com/t/openalias-should-we-invest-in-it-this-year/1833)
-	Strengthening resilience by creating another instance of ABE explorer
-	Native support for Bitcoin and other altcoins, basically multi-coin wallet
-	Smart contracts (e.g. ability for delayed payments based on block height or a transactions occurring after certain amount in a specific address arrives)
-	[IFTTT support](https://en.wikipedia.org/wiki/IFTTT) (e.g. "when payment received send tweet")
