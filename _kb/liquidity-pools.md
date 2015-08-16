---
title: Liquidity Pools
nav_heading: Liquidity Pools
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

### Managed pool

Managed pools are maintained by a person or persons. Liqudity funds are sent to someone who will use them to maintain the peg on behalf of the user. The first example of a managed liquity pool was created by [Henry](https://discuss.nubits.com/users/henry) of the NuBits forum on [Feb 27th, 2015](https://discuss.nubits.com/t/passed-motion-to-create-the-first-liquidity-pool-the-nu-lagoon/1616).

### Un-Managed pool

Un-managed pools (also known as "trustless-liquidity pools") are a Nu community innovation pioneered by [Creon](https://discuss.nubits.com/users/creon) of the NuBits forum. The first implementation of an un-managed pool was [announced on March 5th 2015](https://discuss.nubits.com/t/trust-less-liquidity-pool/1686). The design of the unmanaged pool is intended to significalty reduce the counter-party risk involved to pool contriubters by keeping funds in their control. This first implementation uses a client/server architecture. A pool operator runs the server software that clients can connect to. The job of the server is to verify that users have orders places on NuBits supported exchanges that help support the NuBits peg. The client software automatically places these orders and reports them back to the server. Clients compete with each other to provide liquidity, and earn interest paid out by the server for the support they provide. Anyone can join or leave an un-managed pool at their own discretion. 

## How do I dive in?

Various pools are listed [HERE](https://nubits.com/liquidity-pools) on the NuBits website.