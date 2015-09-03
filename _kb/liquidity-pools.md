---
title: Liquidity Pools
nav_heading: NuBits
filename: liquidity-pools.md
permalink: /liquidity-pools/
layout: kb
lang: en
callouts:

---

Liquidity pools are a community driven innovation of the Nu Network to help support the NuBits peg.

## How does it work?

In the same way that anyone can contribute hashing power to help maintain the bitcoin network, anyone can contribute liquidity to help support the NuBits $1 peg. People who provide liquidty to support the peg can earn interest back for helping to maintain it.

## Types of liquidity pools

### Managed liquidity pool (MLP)

Managed pools are maintained by a person or persons. Liqudity funds are sent to someone who will use them to maintain the peg on behalf of the user. The first example of a managed liquity pool was created by [Henry](https://discuss.nubits.com/users/henry) of the NuBits forum on [Feb 27th, 2015](https://discuss.nubits.com/t/passed-motion-to-create-the-first-liquidity-pool-the-nu-lagoon/1616).

Examples:

 * [nulagoon.com](http://nulagoon.com/)

### Automated liquidity pool (ALP)

Automated pools (also known as "trustless-liquidity pools") are a Nu community innovation pioneered by [Creon](https://discuss.nubits.com/users/creon) of the NuBits forum.  


The first implementation of an automated pool was [announced on March 5th 2015](https://discuss.nubits.com/t/trust-less-liquidity-pool/1686). The design of the automated pool is intended to significantly reduce the counter-party risk involved to pool contriubters by keeping funds in their control. This first implementation uses a client/server architecture. A pool operator runs the server software that clients can connect to. The job of the server is to verify that users have orders placed on NuBits supported exchanges that help support the NuBits peg. The client software automatically places these orders and reports them back to the server. Clients compete with each other to provide liquidity, and earn interest paid out by the server for the support they provide. Anyone can join or leave an automated pool at their own discretion. 

#### Source code

The code for the ALP is open source, and so implementations can vary across pools.

Two examples of automated pool software currently in use can be found below.

 * [nupool.net](http://nupool.net) source code is available [HERE](https://github.com/inuitwallet/nu-pool)
 * [nupond.net](http://nupond.net) source code is available [HERE](https://github.com/Nagalim/nu-pool)

## How do I dive in?

Various pools are listed [HERE](https://nubits.com/liquidity-pools) on the NuBits website.

## Need some help, or have more questions?

Check out the liquidity pool discussions [HERE](https://discuss.nubits.com/c/liquidity-pools) on the official NuBits forum.
