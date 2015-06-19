Coming soon. 
[block:api-header]
{
  "type": "basic",
  "title": "Background"
}
[/block]
NuNet is a distributed network of computers that store and exchange a lot of information.  At the current state the information is mostly computer-friendly.  However, the network must be managed by humans who need to take critical decisions according to the NuNet underlying data.

NuWebService structures the available information and makes it available through a json API.
[block:api-header]
{
  "type": "basic",
  "title": "Information Structure"
}
[/block]
* Custodial grants information : Where proposed NuBit grants are being directed, and the level of support that exists for them.
* Liquidity pool information : It display the current liquidity pool information, i.e. the amount of NuBits being sold and bought on open markets.  This information is essential to shareholders that needs to take decisions and vote on interest rates and custodial grants.   The most important information is the rate buy liquidity / sell liquidity.  
* NuBits parking information : This information is essential for people that wants to buy and park nubuts. The information si twofold since it contains :
  * What interest rates are being voted on as the most preferential for the network, and for what length of time. Interest rates are functions of time, and as such I imagine we will have to chart the interest rates against the time.
  * An overview on over parked NuBits (  number of NuBits presently parked,  total number of NuBits parked and the percentage of NuBits parked relative to the total NuBits supply, the length of time remaining on the largest blocks of parked NuBits )
* Motions information:  What the most popular motions are at any given time, and the level of support that exists for them. The motion should also hyperlink to the actual text of the motion - whether that is on a forum or in the client, I am not yet sure.