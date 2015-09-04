---
title: NuBot parametric Orderbook
nav_heading: NuBot
filename: parametric-orderbook.md
permalink: /parametric-orderbook/
layout: kb
lang: en
callouts:
---
## Introduction

Before NuBot v0.3.1, we used to put all the available liquidity in a large single order, according to the initial design outlined in the whitepaper. Starting from NuBot v0.3.2 and following the evolution of liquidity operation (read community discussions  [one](https://discuss.nubits.com/t/finalized-evolution-of-liquidity-operations/618) - [two](https://discuss.nubits.com/t/nubits-trading-walls-design-features-and-the-improvements-chinese/1066) - [three](https://discuss.nubits.com/t/closed-motion-to-cease-shareholder-funded-nbt-ppc-operations/702) ) the bot implements the [multi-tier liquidity model](https://docs.nubits.com/nubits-liquidity/). 

In this model, NuBot places the vertical walls at the best price (Tier1) along with a tail of orders distributed at premium prices and controlled by bot operators : the parametric order book.  

By managing liquidity this way operators can mitigate risks of being exposed to volatility and malicious actors while still providing a solid 1$ peg.

## Parametric orderbook

The model is simple and at the same time flexible enough for making it fit in different market scenarios. 
![Orderbook](https://bitbucket.org/repo/ordrAX/images/2225183234-Screen%20Shot%202015-08-06%20at%2012.23.49.png)



 - The model can be configured by the custodian using the configuration file or directly in the UI.
 - The model is dynamic, in the sense that its parameters can be manipulated at runtime.
 - NuBot will implement capabilities to autonomously adapt parameters to best fit market conditions.
 - The buy and sell liquidity can be modelled separately

If you launch NuBot with the GUI, you will be able to change parameters and see a real time preview of how changing parameters affects the sahpe of your orderbook.
**The options below are not required and we highly suggest to omit them. NuBot will use the default options automatically.**

| Parameter      |  Default value  |  Description  |   Admitted values  | 
| ------------- |:-------------:| -------------:| -------------:| 
| bookDisabletier2 | false | if set to true, will only place the tier1 walls  |  boolean |
| bookSellwall | 500 | maximum volume to put on sell walls at best price (tier1) |  double , expressed in NBT ; 0 allowed |
| bookBuywall | 500 | maximum volume to put on buy walls at best price (tier1) |  double , expressed in NBT ; 0 allowed |
| bookSellOffset | depends on currency (0;0.01;0.025) | offset from target price  |  double , expressed USD.  |
| bookBuyOffset | depends on currency (0;0.01;0.025) |  offset from target price  |  double , expressed USD.  |
| bookSellInterval | 0.008 |  interval price between two sell orders  |  double , expressed USD. (0.000001,0.3)  |
| bookBuyInterval | 0.008 |  interval price between two buy orders  |  double , expressed USD. (0.000001,0.3) |
| bookSellType | exp | shape of the curve  |  String , **lin**ear; **exp**onential; **log**arithmic;  |
| bookBuyType | exp | shape of the curve  |  String , **lin**ear; **exp**onential; **log**arithmic; |
| bookSellSteepness | mid | steepness of the curve  |  String , flat;low;mid;high |
| bookBuySteepness | mid | steepness of the curve  |  String , flat;low;mid;high  |



Below, a sample JSON representation of the model, to add to custodian configuration file. 
{% highlight text %}
{
  "bookDisabletier2": false,
  
  "bookSellWall": 1000.0,
  "bookSellOffset": 0.002,
  "bookSellInterval": 0.015,
  "bookSellType": "exp",
  "bookSellSteepness": "low",

  "bookBuywall": 1000.0,
  "bookBuyOffset": 0.048,
  "bookBuyInterval": 0.015,
  "bookBuyType": "log",
  "bookBuySteepness": "low"
}
{% endhighlight %}
