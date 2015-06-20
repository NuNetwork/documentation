---
title: RPC API
nav_heading: Technical Resources
filename: rpc-api.md
permalink: /rpc-api/
layout: kb
lang: en
callouts:
---


## Nu Network Ports

{% highlight bash %}
PROTOCOL PORT 7890
// Base RPC port used by the NuShares RPC server.
// Other unit RPC servers listen on RPC_PORT+1, RPC_PORT+2, etc.
RPC PORT 14001
RPC PORT 14002     // NuBits

// Same rules apply to testnet, but on different ports
TESTNET PORT 7895
TESTNET RPC PORT 15001     // NuShares
TESTNET RPC PORT 15002     // NuBits

// Peercoin ports used when communicating with the Peercoin wallet for dividend distributions
PEERCOIN RPC PORT 9902
PEERCOIN TESTNET RPC PORT 9904
{% endhighlight %}

## Methods

### addmultisigaddress

`addmultisigaddress <nrequired> <'["key","key"]'> [account]`

Add a nrequired-to-sign multisignature address to the wallet


### backupwallet

`backupwallet <destination>`

Safely copies wallet.dat to destination, which can be a directory or a path with filename.


### checkwallet

`checkwallet`

Check portfolio for integrity.


### createmultisig

`createmultisig nrequired ["key",...]`


### createrawtransaction

`createrawtransaction [{"txid":txid,"vout":n},...] {address:amount,...}`

Create a transaction spending given inputs


### decoderawtransaction

`decoderawtransaction <hex string>`

Return a JSON object representing the serialized, hex-encoded transaction.


### distribute

`distribute <cutoff timestamp> <amount> [<proceed>]`

cutoff is date and time at which the share balances should be considered. Format is unix time.



### dumpprivkey

`dumpprivkey <ppcoinaddress>`

Reveals the private key corresponding to <ppcoinaddress>.

### encryptwallet

` encryptwallet <passphrase>`

Encrypts the portfolio with <passphrase>

### exportpeercoinkeys

`exportpeercoinkeys`

Add the Peercoin keys associated with the NuShares addresses to the Peercoin wallet. Peercoin must be running and accept RPC commands.



### getaccount

`getaccount <address>`

Returns the account associated with the given address.



### getaccountaddress

`getaccountaddress <account>`

Returns the current Nu address for receiving payments to this account.



### getaddressesbyaccount

`getaddressesbyaccount <account>`

Returns the list of addresses for the given account.



### getbalance

`getbalance [account] [minconf=1]`

If [account] is not specified, returns the server's total available balance.



### getblock

`getblock <hash> [txinfo]`

txinfo optional to print more detailed tx info



### getblockcount

`getblockcount`

Returns the number of blocks in the longest block chain.



### getblockhash

`getblockhash <index>`

Returns hash of block in best-block-chain at <index>.



### getblocktemplate

`getblocktemplate [params]`

Returns data needed to construct a block to work on:



### getcheckpoint

`getcheckpoint`

Show info of synchronized checkpoint.



### getconnectioncount

`getconnectioncount`

Returns the number of connections to other nodes.



### getcustodianvotes

`getcustodianvotes [<block height>] [<block quantity>]`

Returns an object containing the custodian vote results.



### getdifficulty

`getdifficulty`

Returns difficulty as a multiple of the minimum difficulty.



### getgenerate

`getgenerate`

Returns true or false.



### gethashespersec

`gethashespersec`

Returns a recent hashes per second performance measurement while generating.



### getinfo

`getinfo`

Returns an object containing various state info.



### getliquidityinfo

`getliquidityinfo <currency>`

currency is the single letter of the currency (currently only 'B')



### getmininginfo

`getmininginfo`

Returns an object containing mining-related information.



### getmotions

`getmotions [<block height>] [<block quantity>]`

Returns an object containing the motion vote results.



### getnetworkghps

`getnetworkghps`

Returns a recent Ghash/second network mining estimate.



### getnewaddress

`getnewaddress [account]`

Returns a new Nu address for receiving payments.  If [account] is specified (recommended), it is added to the address book so payments received with the address will be credited to [account].



### getparkrates

`getparkrates [<height>] [<currency>]`

Returns an object containing the park rates in the block at height <height> (default: the last block).



### getpeercoinaddresses

`getpeercoinaddresses <account>`

Returns the list of addresses and the associated Peercoin address for the given account.



### getpeerinfo

`getpeerinfo`

Returns data about each connected network node.



### getrawmempool

`getrawmempool`

Returns all transaction ids in memory pool.



### getrawtransaction

`getrawtransaction <txid> [verbose=0]`

If verbose=0, returns a string that is



### getreceivedbyaccount

`getreceivedbyaccount <account> [minconf=1]`

Returns the total amount received by addresses with <account> in transactions with at least [minconf] confirmations.



### getreceivedbyaddress

`getreceivedbyaddress <address> [minconf=1]`

Returns the total amount received by <address> in transactions with at least [minconf] confirmations.



### gettransaction

`gettransaction <txid>`

Get detailed information about <txid>


### gettxout

`gettxout "txid" n ( includemempool )`


### getvote

`getvote`

Returns the vote that will be inserted in the next proof of stake block.



### getwork

`getwork [data]`

If [data] is not specified, returns formatted hash data to work on:



### help

`help [command]`

List commands, or get help for a command.



### importprivkey

`importprivkey <ppcoinprivkey> [label]`

Adds a private key (as returned by dumpprivkey) to your wallet.



### keypoolrefill

`keypoolrefill`

Fills the keypool, requires portfolio passphrase to be set.



### liquidityinfo

`liquidityinfo <currency> <buyamount> <sellamount> <grantaddress>`

Broadcast liquidity information.



### listaccounts

`listaccounts [minconf=1]`

Returns Object that has account names as keys, account balances as values.



### listparked

`listparked [account]`

Returns the list of parked coins.



### listreceivedbyaccount

`listreceivedbyaccount [minconf=1] [includeempty=false]`

[minconf] is the minimum number of confirmations before payments are included.



### listreceivedbyaddress

`listreceivedbyaddress [minconf=1] [includeempty=false]`

[minconf] is the minimum number of confirmations before payments are included.



### listsinceblock

`listsinceblock [blockhash] [target-confirmations]`

Get all transactions in blocks since block [blockhash], or all transactions if omitted



### listtransactions

`listtransactions [account] [count=10] [from=0]`

Returns up to [count] most recent transactions skipping the first [from] transactions for account [account].



### listunspent

`listunspent [minconf=1] [maxconf=9999999]  ["address",...]`

Returns array of unspent transaction outputs



### makekeypair

`makekeypair [prefix]`

Make a public/private key pair.



### move

`move <fromaccount> <toaccount> <amount> [minconf=1] [comment]`

Move from one account in your portfolio to another.



### park

`park <amount> <duration> [account=""] [unparkaddress] [minconf=1]`

<amount> is a real and is rounded to the nearest 0.000001



### repairwallet

`repairwallet`

Repair portfolio if checkwallet reports any problem.



### reservebalance

`reservebalance [<reserve> [amount]]`

<reserve> is true or false to turn balance reserve on or off.



### sendalert

`sendalert <message> <privatekey> <minver> <maxver> <priority> <id> [cancelupto]`

<message> is the alert text message



### sendfrom

`sendfrom <fromaccount> <toaddress> <amount> [minconf=1] [comment] [comment-to]`

<amount> is a real and is rounded to the nearest 0.000001



### sendmany

`sendmany <fromaccount> {address:amount,...} [minconf=1] [comment]`

amounts are double-precision floating point numbers



### sendrawtransaction

`sendrawtransaction <hex string> [checkinputs=0]`

Submits raw transaction (serialized, hex-encoded) to local node and network.



### sendtoaddress

`sendtoaddress <address> <amount> [comment] [comment-to]`

<amount> is a real and is rounded to the nearest 0.000001



### setaccount

`setaccount <address> <account>`

Sets the account associated with the given address.



### setgenerate

`setgenerate <generate> [genproclimit]`

<generate> is true or false to turn generation on or off.



### setmotionvote

`setmotionvote <motion hash>`

<motionhash> is the hash of the motion to vote for.



### setvote

`setvote <vote>`

<vote> is the complete vote in JSON. Example:

```
setvote {
   "custodians":[
      {
         "address":"bPwdoprYd3SRHqUCG5vCcEY68g8UfGC1d9",
         "amount":100.00000000
      },
      {
         "address":"bxmgMJVaniUDbtiMVC7g5RuSy46LTVCLBT",
         "amount":5.50000000
      }
   ],
   "parkrates":[
      {
         "unit":"B",
         "rates":[
            {
               "blocks":8192,
               "rate":0.00030000
            },
            {
               "blocks":16384,
               "rate":0.00060000
            },
            {
               "blocks":32768,
               "rate":0.00130000
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
### signmessage

`signmessage <address> <message>`

Sign a message with the private key of an address



### signrawtransaction

`signrawtransaction <hex string> [{"txid":txid,"vout":n,"scriptPubKey":hex},...] [<privatekey1>,...] [sighashtype="ALL"]`

Sign inputs for raw transaction (serialized, hex-encoded).



### stop

`stop`

Stop Nu server.



### submitblock

`submitblock <hex data> [optional-params-obj]`

[optional-params-obj] parameter is currently ignored.



### unpark

`unpark`

unpark all transaction that have reached duration



### validateaddress

`validateaddress <address>`

Return information about <address>.



### verifymessage

`verifymessage <address> <signature> <message>`

Verify a signed message



### walletlock

`walletlock`

Removes the portfolio encryption key from memory, locking the portfolio.



### walletpassphrase

`walletpassphrase <passphrase> <timeout> [mintonly]`

Stores the portfolio decryption key in memory for <timeout> seconds.



### walletpassphrasechange

`walletpassphrasechange <oldpassphrase> <newpassphrase>`

Changes the portfolio passphrase from <oldpassphrase> to <newpassphrase>.
