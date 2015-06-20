---
title: Hosting a data feed
nav_heading: NuShares
filename: hosting-a-data-feed.md
permalink: /hosting-a-data-feed/
layout: kb
lang: en
callouts:
---

##Feed URL

Data feeds can be pulled into the client using a URL that points to the raw JSON voting data. The client accepts JSON voting data using the same format as the **setvote** RPC command.

In the example below there are two custodian votes, three park rate votes, and two motion votes. Having this data hosted somewhere like http://myvotingdata.com/votes.json allows NuShares holders to enter the URL into their client and pull in the voting data. The client pulls the data every 60 seconds by default, but this can be changed.

```
{
   "custodians":[
      {
         "address":"bPwdoprYd3SRHqUCG5vCcEY68g8UfGC1d9",
         "amount":100.0
      },
      {
         "address":"bxmgMJVaniUDbtiMVC7g5RuSy46LTVCLBT",
         "amount":5.5
      }
   ],
   "parkrates":[
      {
         "unit":"B",
         "rates":[
            {
               "blocks":8192,
               "rate":0.0003
            },
            {
               "blocks":16384,
               "rate":0.0006
            },
            {
               "blocks":32768,
               "rate":0.0013
            }
         ]
      }
   ],
   "motions":[
      "8151325dcdbae9e0ff95f9f9658432dbedfdb209",
      "3f786850e387550fdab836ed7e6dc881de23001b"
   ]
}
```

Since the client only requires a simple URL to the raw JSON there’s a number of hosting services that can be used to provide the data feed. Here’s an example using github.

https://github.com/CoinGame/CoinGame-NuVotes-Testnet

One advantage to using a service like this is that a running public history of vote changes will be available in the commit history.

##URL Signature

To prevent man-in-the-middle attacks data feed sources may also provide a secondary URL that points to the signature of the voting data, and the NuShares address used to sign it. These two additional pieces of information can help assure that votes have not changed while traveling to the client. The client will throw an error if a change has been noticed and the vote will not be changed.

##votenotify configuration

Providing **votenotify** the path to a script in your conf file will invoke that script when votes are changed. For feed providers this can be used to automatically update hosted voting data when the feed provider manually changes votes. Here's a sample script that generates the voting data and vote signature with a supplied NSR address.
```
#!/bin/bash

NUD=/path/to/nud
ARGS="-testnet"
VOTE_PATH=/path/to/output/vote.json
SIGNATURE_PATH=/path/to/output/vote.json.signature
ADDRESS=S....

$NUD $ARGS getvote >$VOTE_PATH
$NUD $ARGS signmessage $ADDRESS <$VOTE_PATH >$SIGNATURE_PATH
```

Example conf file:
```
server=1
rpcuser=test123
rpcpassword=test321
votenotify=/home/user/votenotify.sh
```
