---
title: NuWebService
nav_heading: Nu Web Services
filename: nuwebservice.md
permalink: /nuwebservice/
layout: kb
lang: en
callouts:
---

Coming soon.

## Background

NuNet is a distributed network of computers that store and exchange a lot of information. At the current state the information is mostly computer-friendly. However, the network must be managed by humans who need to take critical decisions according to the NuNet underlying data.

NuWebService structures the available information and makes it available through a JSON API.

## Information Structure

* **Custodial Grants Information**:  
Where proposed NuBit grants are being directed, and the level of support that exists for them.  
* **Liquidity Pool Information**:
Display the current liquidity pool information, i.e. the amount of NuBits being sold and bought on open markets. This information is essential to shareholders that needs to take decisions and vote on interest rates and custodial grants. The most important information is the rate buy liquidity / sell liquidity.  
* **NuBits Parking Information**:  
This information is essential for people who want to buy and park NuBits. The information is twofold and contains :  
  * What interest rates are being voted on as the most preferential for the network, and for what length of time. Interest rates are functions of time, and as such we imagine we will have to chart the interest rates against the time.  
  * An overview of parked NuBits (number of NuBits presently parked, total number of NuBits parked and the percentage of NuBits parked relative to the total NuBits supply, the length of time remaining on the largest blocks of parked NuBits).  
* **Motions Information**:  
What the most popular motions are at any given time, and the level of support that exists for them. The motion should also hyperlink to the actual text of the motion - the design decision for whether that is on a forum or available from within the client is still being made.
