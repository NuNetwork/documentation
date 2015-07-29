---
title: NuBits Discourse Assistant Bot
nav_heading: Tools
filename: nbt-discourse-assistantbot.md
permalink: /nubits-discourse-bot/
layout: kb
lang: en
callouts:
---
NuBits Discourse Assistant Bot it is designed to be used on [NuBits official forum](https://discuss.nubits.com)  to retrieve information about NuNet (liquidity, custodians, votes...)  formatting Motions or Custodian proposals and tipping NuBits on the forum.  Just mention `@assistant` in a public discussion or send a PM to access the bot (scroll down for the list of commands).

It comes as a [discourse](http://www.discourse.org/) plugin and its code is open source and can be found  [on bitbucket](https://bitbucket.org/mj2p/assistantbot). 

As well as helping in the formatting of motions , the bot can also fetch any of the NuNet information available in the Nu client and present it here in any public topic. Things like the current liquidity, the current difficulty, the current state of a particular motion or the current park rates can all be accessed with a simple command.
Because the bot is hooked into the Nu Network, it can also let any user tip NuBits to any other user on this forum. To get started with tipping, send a PM with the word 'register' to [assistant](https://discuss.nubits.com/users/assistant/activity) . If you send someone who hasn't registered a tip, I'll create them an account and let them know a tip is waiting for them.

To help get started, below  there is a list of the commands the bot will respond to. Please note that the bot will only respond to 'Private Message' commands via private message. Mention commands will only work when you mention its name in a forum post and type the command as shown below.

## Private Message Commands
Access these command by writing a private message to the user [assistant](https://discuss.nubits.com/users/assistant/activity)  :  

 - `about` : shows bot info.
 - `help` : shows this help screen.

### Formatting Commands

 - `motion hash [motion]` : Hash a motion into the preferred format. (More details below)
 - `custodian hash [address] [amount] [text]` : Hash a Custodian Proposal into the preferred format.

### Tipping Private Message Commands

 - `register` : Register for tipping.
 - `info` : Get your current balance and deposit address
 - `history` : Get the transaction and tipping history of your tipping account
 - `withdraw [address]` : Withdraw your entire balance from the tipping account to [address]
 - `keywords` : Show a list of the keywords which can be used in place of an amount when tipping

## Mention Commands

Mention the bot in a public discussion using `@assistant`

- `@assistant liquidity` : Get the current liquidity information
- `@assistant block count` : Get the current block count
- `@assistant block hash [index]` : Get the hash for the [index] block
- `@assistant custodian votes` : Get the latest Custodian Votes
- `@assistant custodian vote [address]` : Get the vote details for the Custodian address [address]
- `@assistant motion votes` : Get the latest Motion Votes
- `@assistant motion vote [motion_hash]` : Get the vote details for the motion with hash [motion_hash]
- `@assistant park rates` : Get the latest Park Rate values
- `@assistant park rate votes` : Get the latest Park Rate Votes
- `@assistant verify` : Scan the thread for motions and custodial proposals and verify that their hashes are unchanged
- `@assistant qrcode [address]` : Create a QR Code of the valid NBT address.
- `@assistant tip [amount] @[user]` : Send a tip of [amount] NBT to @[user].


## Standardise motion texts 

The main aim is to standardise the format of motions and custodial grants in a way that will allow other future tools to scrape the data from this forum and present it elsewhere. There has been an idea floating around for a web service which allows for data feed generation with a few clicks of a mouse. Such a web service could also act as a repository for motions and custodial proposals so that the data around the activity of NuNet can be easily accessed. A typical use case of Shareholder that wants to propose and hash a motion. 

1. Shareholder wishes to propose a motion. 
2. Shareholder composes motion away from site. 
3. Shareholder sends Pm to Assistant with the motion (see command below)
4. Shareholder clicks on 'verify' link in the reply from Assistant and copies the entire text.
5. Shareholder starts new topic and pastes the copied text into the post. They can then add any other text they want but that won't be included in the hash

The instruction next to the verify link, to copy everything including the tags in instruction for if you want to independently verify the hash with a tool that isn't Assistant bot. When calculating the hash, assistant uses the raw text contained by the tags. By copying just that portion of the raw text, any other tool that calculates RIPEMD160 hashes should return the same value.


To use Assistant to format a motion, send a PM to @assistant. the first two words of the message should be 'motion hash'. Any other text in the message will be treated as the motion text and will be formatted into a standard motion.

`motion hash this is my motion`

Once correctly formatted, Assistant will calculate the RIPEMD160 hash of the motion text and will reply to your PM with the text for your post.

{% highlight text %}
Motion RIPEMD160 hash: 886c36dd00ebdf8f87812d141ba941e053c21830

=##=##=##=##=##=## Motion hash starts with this line ##=##=##=##=##=##=

this is my motion


=##=##=##=##=##=## Motion hash ends with this line ##=##=##=##=##=##=
{% endhighlight %}

To copy that text you need to click the 'Verify' link towards the bottom of Assistant reply. This shows you the raw text that was hashed. If you paste that raw text, in it's entirety, into your post, it will appear nicely formatted as it did in Assistant reply. 
If you don't copy the raw 'verify' text, your post won't be nicely formatted and the verification text will fail the hash if any one checks.

Assistant adds some hidden html tags to the formatted motion which will allow future tools to easily access information.

To verify a motion hash, reply to a motion post, mention @assistant and follow immediately with the word 'verify'. 

`@assistant verify hash this is my motion`

Assistant will scan the entire thread for any motions and re-calculate the hash on each. This provides a nice, easy way to verify that a motions text hasn't changed and that you are voting for the correct thing in your Nu client.

