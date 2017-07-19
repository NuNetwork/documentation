---
title: Glossary
nav_heading: Getting Started
filename: glossary.md
permalink: /glossary/
layout: kb
lang: en
callouts:
---
## Nu Terms

### Nu Network (Nu/NuNet)

The whole Nu entity. This is includes the code, assets, communities, and services that allow the network to function.

### NuBit (?-NBT)

NuBits first and primary currency asset representing a digital US Dollar.

- United States NuBits (US-NBT) [pegged](#peg) to the US dollar.  

The following assets do not exist yet, but [have been voted on](https://discuss.nubits.com/t/passed-motion-to-introduce-new-nubits-products/2834) by NuShares holders to be implemented in the future.  

- Chinese NuBits (CN-NBT) pegged to the Chinese yuan.
- European NuBits (EU-NBT) pegged to the European euro.
- SDR NuBits (X-NBT) pegged to the [Special Drawing Rights](https://www.imf.org/external/np/fin/data/rms_sdrv.aspx) basket currency.

### NuShare (NSR)

An asset that represents ownership of Nu and provides the ability to vote and control the Nu network in a distributed fashion.

Minting owners of NuShares are first rewarded as the Nu network generates blocks via a 40 NSR block generation reward. Then NSR Shareholders are further rewarded for network profits (NuBits health) by either distribution of dividends, network NSR share buybacks and/or a combination of the two methods.

### NuShareholder

An individual (or other entity) owning NuShares, and as such Nu.

### NuBot

A cross-platform automated trading bot written in Java.

### PyBot

A client–server pair that performs automated trading and order validation. Written in Python, it is the first iteration of [automated liquidity pool (ALP)](#automated-liquidity-pool-alp) software.

### First Strategic Reserve Team (FSRT)

A team of several individuals entrusted with Nu assets, protected with [multisig](#multisignature-multisig), that can be bought or sold on the open market manually should circumstances emerge that can not be handled by the liquidity pools.

### First Liquidity Operations Team (FLOT)

A group of elected individuals that hold the private keys to [multisignature](#multisignature-multisig) addresses containing funds owned by Nu.

### Distributed Autonomous Organization/Company/Corporation (DAO/DAC)

An organization that has no specific physical geographical location or headquarters, and takes action through consensus.

#### Definitions

- [Wikipedia](https://en.wikipedia.org/wiki/Decentralized_autonomous_organization)
- [Vitalik Buterin](https://blog.ethereum.org/2014/05/06/daos-dacs-das-and-more-an-incomplete-terminology-guide/)

### Custodian

An individual or other entity which controls an address that has had new NuBits or NuShares created at it as part of a successful custodian grant vote. These NuBits or NuShares are created by the network, not transferred from a different address.

### Sell Side (Ask) and Buy Side (Bid)

On an exchange order book, the sell side is comprised of all orders that offer to sell the item being exchanged. Conversely, the buy side (bid) is comprised of all orders offering to buy the exchanged item. The price of the item can be said to be midway between the highest buy/bid order and the lowest sell/ask order. The gap between the top bid and bottom ask orders is called the [spread](#spread).

### Sell-Side Custodian

A term coined in the Nu [white paper](https://nubits.com/learn/white-paper). A sell-side custodian sells their granted NuBits on an exchange and returns the profits to Nu in the form of dividends. A buy-side custodian on the other hand, immediately places orders to buy NuBits, thus supporting the buy side.

## Liquidity Terms

### Liquidity

The ability to buy or sell an asset quickly and with no or minimal impact to the market value of the asset.

### Liquidity Tier

Describes where Nu's funds lie.

- **Tier 1** is immediately available funds in an order book on an exchange.
- **Tier 2** is funds on an exchange that are not placed on the order book, or is placed on the orderbook at premium prices. It can be promoted to tier 1 within seconds (by bots).
- **Tier 3** is funds in the hands of custodians that are not on an exchange, but available enough to quickly be moved to one.
- **Tier 4** is funds under control by different groups or entities on mission for Nu, like [FLOT](#first-liquidity-operations-team-flot) and [FSRT](#first-strategic-reserve-team-fsrt). Currently expected to be available within around a day or two.
- **Tier 5** presents itself in a decentralized manner through the manipulation of interest rates (park rates). It is generally buy side, although technically it can be sell side in the case of lowering interest rates. It's available in days and the cost takes the form of interest paid.
- **Tier 6** takes the form of custodial grants for sell side, and currency burning for buy side (presuming a currency burning motion is passed and implemented). It takes a week or more to bring to market but has zero maintenance costs.

As you move from lower tiers to higher tiers, the funds are increasingly difficult to bring to market to directly support the peg, but conversely, they suffer less risk (exchange default, rogue custodian etc.). By balancing the funds in the different tiers, Nu can control the available liquidity while mitigating some of the associated risk.

### Liquidity Provider (LP)

A person, team, or technology that enables the buyers and sellers of an asset to transact efficiently with no (or minimal) impact to the market value.

### Liquidity Providing Custodian (LPC)

A [custodian](#custodian) granted NuBits with the sole intention of providing them to market, i.e. sell them on an exchange supporting Nu's sell side.

### Automated Liquidity Pool (ALP)

A distributed autonomous entity that coordinates the placement and pricing of assets that are owned by individuals on an exchange, to provide liquidity in a unified fashion. The ALP rewards the risk that the individuals are taking by coordinating the buy-side and sell-side walls in a way that a small profit is earned from the spread.

*Previously called Trustless Liquidity Pool (TLLP).*

### Managed Liquidity Pool (MLP)

Participants provide their assets to a trusted entity, who then manages the pricing and placement of the assets on an exchange to provide liquidity. The MLP provides compensation for the risk taken by individuals either with a spread between buy-side and sell-side walls, or by requesting and distributing NuBits or NuShares received via a successful custodian vote.

### Trustless Liquidity Pool (TLLP)

Old term for [Automated Liquidity Pool (ALP)](#automated-liquidity-pool-alp).


## Economics Terms

### Buy/Sell Wall

A large order on an exchange order book. When viewing an order book as a graph (called a depth chart on most exchanges) a large order can be seen as a large jump in the volume and looks a bit like a wall. When the price is moving and orders are being filled, the price will stall once it hits the large order as it will take some time to fill, almost as if the price movement “hit a wall”.

Nu has traditionally used “walls” as a way to control the price of NuBits. Large buy and sell orders just above and just below $1.00 prevent the price from moving too far from that price.

### Peg

Both abstractly and concretely affixing the price of one unit of account to another such that they are interchangable economically. A peg is assumed to have a well-defined price feed.

### Spread

The difference in percent (%) between the bid and ask on an orderbook. The baseline, or divisor in the percentage calculation, is the price feed.

### Spread After Fees (SAF)

Usually a term used by pool operators. The spread minus twice the trading fee on the exchange represents the profit earned by the liquidity provider in an ideal case where the price feed does not change and there is both buying and selling.

### Tolerance

The band about the price feed in which an order can be placed and still be credited by an [automated liquidity pool (ALP)](#automated-liquidity-pool-alp).

### Deviation

The relative amount the price feed must change by in order to cause a bot to remove orders on the order book.

## Cryptocoin Terms

### Multisignature (Multisig)

A method for multiple parties to keep coins in an address and only release those coins with an initially specified number of parties agreeing to the transaction.

As example, a 3-of-5 multisig address would require (any) three of the five owners to sign a transaction to move coins out of the address.
