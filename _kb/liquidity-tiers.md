---
title: NuBits Liquidity Guide
nav_heading: NuBits
filename: liquidity-tiers.md
permalink: /nubits-liquidity/
layout: kb
lang: en
callouts:
---

A motion was put forth by Jordan Lee on [Nov 12th 2014](https://discuss.nubits.com/t/finalized-evolution-of-liquidity-operations/618) to help guide the development of liquidity operations for the Nu Network. The design calls for recognizing six tiers to the liquidity operations that support the NuBits $1 peg.

## NuBits Liquidity Tiers

### Tier 1

This liquidity is immediately available, being on the order book at the best price (1$ +- fees and spread). It is used by NuBot to maitain the 1$ peg on exchanges.

### Tier 2

This liquidity sits on exchanges but is not usually placed on order books, or is placed on the orderbook at premium prices. It can be promoted to the order book (Tier 1) in a couple seconds.

### Tier 3

This liquidity sits off exchange and is held by liquidity providers in wallets not exposed to counterparty risk or the risk of NuBot malfunction. It can be promoted to tier 2 when needed in minutes.

### Tier 4

This liquidity can be provided by custodians not dedicated to liquidity operations. A present example are the proceeds of NuShare sales. They are intended for operational and development expenses, but can be used to support the critical function of liquidity provision as needed. When these funds are used for liquidity, they are exchanged from one type of asset to another, but are still available for their original purpose, such as development. These funds can be promoted to tier 3 in hours and the cost is exchange rate risk.

### Tier 5

This liquidity presents itself in a decentralized manner from the manipulation of interest rates (park rates). This liquidity is generally buy side, although technically it can be sell side in the case of lowering interest rates. This liquidity is available in days and the cost takes the form of interest paid.

### Tier 6

This liquidity takes the form of custodial grants for sell side and currency burning for buy side (presuming a currency burning motion is passed and implemented as appears likely). It takes a week or more to bring to market but has zero maintenance costs. 
