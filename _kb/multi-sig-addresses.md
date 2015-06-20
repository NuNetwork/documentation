---
title: Using multi-sig addresses
nav_heading: Technical Resources
filename: multi-sig-addresses.md
permalink: /multi-sig-addresses/
layout: kb
lang: en
callouts:
---

Creating a multisig address
---------------------------

Each person must create a new address and retrieve the public key:

    ./nud -unit=B getnewaddress
    ./nud -unit=B validateaddress ADDRESS

The public key is displayed in the `pubkey` field. Everyone must send his public key to the others so that everyone can add the multisig script to their wallet.

All the nodes must generate the multisig address. For example to make a 2-of-3 multisig you can run:

    ./nud -unit=B addmultisigaddress 2 '["PUBKEY1", "PUBKEY2", "PUBKEY3"]'

Any fund sent to the address returned by this command will be spendable only if 2 of the 3 keys sign the transaction.


Spending multisig funds
-----------------------

To spend some funds sent to the multisig address you need the transaction ID.
There's no tool right now in the client to retrieve all the transaction IDs associated with an address because the client only keeps track of the transaction it can spend. So you must either use a block explorer or ask the person who sent the funds.

You must also know the output number of the coins you want to spend. To do that you can either use a (detailed) block explorer or use the `getrawtransaction` command:

    ./nud -unit=B getrawtransaction ID_OF_THE_TRANSACTION 1

Search for the `vout` array item of type `scripthash` with the multisig address. Note the `n` field and the `value`. Make sure this output has not already been spent (using a block explorer for example).

Now you can create the transaction:

    ./nud -unit=B createrawtransaction '[{"txid": "ID_OF_THE_TRANSACTION", "vout": OUTPUT_N}]' '{"RECIPIENT_ADDRESS": AMOUNT_TO_SEND, "MULTISIG_ADDRESS": CHANGE_AMOUNT}'

The total amount must be equal to the value of the output you want to spend minus the fee (currently 0.01). Warning: you can easily create a transaction with a huge fee (for example if you forget the change or mistype the amount).

You should get a long hex string. Decode it with this command:

    ./nud -unit=B decoderawtransaction TRANSACTION_HEX

When you're confident the transaction is good, you can send the transaction hex to the first owner of a private keys.
He should inspect the transaction with `decoderawtransaction` and if he approves he can sign the transaction with this command:

    ./nud -unit=B signrawtransaction TRANSACTION_HEX

He will get the hex string of the partially signed transaction. He must send it to the next owner, and so on.
The transaction is fully signed when `signrawtransaction` returns with `complete` set to `true`.

Then anyone can send the fully signed transaction with this command:

    ./nud -unit=B sendrawtransaction TRANSACTION_HEX


Example
-------

On node 1:

    $ ./nud -unit=B getnewaddress
    bDRK91pPSZJmvVSUmF9bGF8z7UunJ3DqUV
    $ ./nud -unit=B validateaddress bDRK91pPSZJmvVSUmF9bGF8z7UunJ3DqUV
    {
        "isvalid" : true,
        "address" : "bDRK91pPSZJmvVSUmF9bGF8z7UunJ3DqUV",
        "ismine" : true,
        "pubkey" : "02d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d3",
        "iscompressed" : true,
        "account" : ""
    }

The public key is 02d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d3.

On node 2:

    $ ./nud -unit=B getnewaddress
    bRySSiUpGd51LDq1QHBLf3Np7QsTV5ZAAX
    $ ./nud -unit=B validateaddress bRySSiUpGd51LDq1QHBLf3Np7QsTV5ZAAX
    {
        "isvalid" : true,
        "address" : "bRySSiUpGd51LDq1QHBLf3Np7QsTV5ZAAX",
        "ismine" : true,
        "pubkey" : "030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf98",
        "iscompressed" : true,
        "account" : ""
    }

The public key is 030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf98.

On all nodes:

    $ ./nud --unit=B addmultisigaddress 2 '["02d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d3", "030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf98"]'
    buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1

The multisig address is buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1.

100 NBT have been sent to this address in transaction [9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996](http://testnet.blockexplorer.nu/transactions/9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996)

The details of the transaction:

    $ ./nud -unit=B getrawtransaction 9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996 1
    {
        "hex" : "010000000fa7335401e4ce6d451fd22c77b43b9be5d7d0c962180170b3eceb72c897fd3475e5720566000000006a47304402206a600e1f7baf0bc455491e164d0de873350accf2acc07e8b7a4d48a4c7454292022064cb096576579773104fae67b9c0727e2190093c9244cbf9b08279639152b979012102361afd29c71d0bc0322e24e7095cc49ef62ccaed359a76b8a06728dcbecae9a3ffffffff02784e5c00000000001976a9149561e5644a7c0db1d27861d3c936035026bb036288ac40420f000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042",
        "txid" : "9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996",
        "version" : 1,
        "time" : 1412671247,
        "locktime" : 0,
        "unit" : "B",
        "vin" : [
            {
                "txid" : "660572e57534fd97c872ebecb370011862c9d0d7e59b3bb4772cd21f456dcee4",
                "vout" : 0,
                "scriptSig" : {
                    "asm" : "304402206a600e1f7baf0bc455491e164d0de873350accf2acc07e8b7a4d48a4c7454292022064cb096576579773104fae67b9c0727e2190093c9244cbf9b08279639152b97901 02361afd29c71d0bc0322e24e7095cc49ef62ccaed359a76b8a06728dcbecae9a3",
                    "hex" : "47304402206a600e1f7baf0bc455491e164d0de873350accf2acc07e8b7a4d48a4c7454292022064cb096576579773104fae67b9c0727e2190093c9244cbf9b08279639152b979012102361afd29c71d0bc0322e24e7095cc49ef62ccaed359a76b8a06728dcbecae9a3"
                },
                "sequence" : 4294967295
            }
        ],
        "vout" : [
            {
                "value" : 604.94000000,
                "n" : 0,
                "scriptPubKey" : {
                    "asm" : "OP_DUP OP_HASH160 9561e5644a7c0db1d27861d3c936035026bb0362 OP_EQUALVERIFY OP_CHECKSIG",
                    "hex" : "76a9149561e5644a7c0db1d27861d3c936035026bb036288ac",
                    "reqSigs" : 1,
                    "type" : "pubkeyhash",
                    "addresses" : [
                        "bSM8ekWuCov3by6JcUZnKFfyohdntEzKEj"
                    ]
                }
            },
            {
                "value" : 100.00000000,
                "n" : 1,
                "scriptPubKey" : {
                    "asm" : "OP_HASH160 c39dbda222a630c5aeaff5fbd4d870d5e63d01ab OP_EQUAL",
                    "hex" : "a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab87",
                    "reqSigs" : 1,
                    "type" : "scripthash",
                    "addresses" : [
                        "buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1"
                    ]
                }
            }
        ],
        "blockhash" : "67130e44bd9043bb6bab05d8b5febe53eabbfb304cad80e2e5cebad5e375bb06",
        "confirmations" : 3,
        "blocktime" : 1412671351
    }

We can see the output 1 was sent to our multisig address. We will send 50 NBT from this output to address bGzbbVhQQRbQcDjTPxrcgifNh3dZjnpbUP and the change back to the multisig address.

    $ ./nud -unit=B createrawtransaction '[{"txid": "9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996", "vout": 1}]' '{"bGzbbVhQQRbQcDjTPxrcgifNh3dZjnpbUP": 50, "buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1": 49.99}'
    010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b0100000000ffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042

Here's our generated transaction:

    $ ./nud decoderawtransaction 0100000089ac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b0100000000ffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042
    {
        "txid" : "ecce5df8b05856236c8de520aab69a5b1425cedfc3dd98941a9cb85aa417c52c",
        "version" : 1,
        "time" : 1412672649,
        "locktime" : 0,
        "unit" : "B",
        "vin" : [
            {
                "txid" : "9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996",
                "vout" : 1,
                "scriptSig" : {
                    "asm" : "",
                    "hex" : ""
                },
                "sequence" : 4294967295
            }
        ],
        "vout" : [
            {
                "value" : 50.00000000,
                "n" : 0,
                "scriptPubKey" : {
                    "asm" : "OP_DUP OP_HASH160 2ec6853a48d497ad2267f83f97abe1b595e1af66 OP_EQUALVERIFY OP_CHECKSIG",
                    "hex" : "76a9142ec6853a48d497ad2267f83f97abe1b595e1af6688ac",
                    "reqSigs" : 1,
                    "type" : "pubkeyhash",
                    "addresses" : [
                        "bGzbbVhQQRbQcDjTPxrcgifNh3dZjnpbUP"
                    ]
                }
            },
            {
                "value" : 49.99000000,
                "n" : 1,
                "scriptPubKey" : {
                    "asm" : "OP_HASH160 c39dbda222a630c5aeaff5fbd4d870d5e63d01ab OP_EQUAL",
                    "hex" : "a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab87",
                    "reqSigs" : 1,
                    "type" : "scripthash",
                    "addresses" : [
                        "buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1"
                    ]
                }
            }
        ]
    }

We can see there's no signature yet because the `scriptSig` field is empty.

On node 1 we sign the raw transaction:

    $ ./nud -unit=B signrawtransaction 010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b0100000000ffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042
    {
        "hex" : "010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b01000000910047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd3530147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852aeffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042",
        "complete" : false
    }

The partially signed transaction is returned in the `hex` field. We must sent this to node 2.

On node 2 we sign the transaction partially signed by node 1:

    $ ./nud -unit=B signrawtransaction 010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b01000000910047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd3530147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852aeffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042
    {
        "hex" : "010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b01000000da0047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd353014830450221008cd54b9d3a58d3b8cc37996016091cc657fdd0f605c765a721f4c61455eba2c5022042fb2133cc28243ca457e93f5645d34592c3c972c7b52731cb12f678e25181680147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852aeffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042",
        "complete" : true
    }

Now the transaction is complete. Here's what it looks like:

    $ ./nud -unit=B decoderawtransaction 010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b01000000da0047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd353014830450221008cd54b9d3a58d3b8cc37996016091cc657fdd0f605c765a721f4c61455eba2c5022042fb2133cc28243ca457e93f5645d34592c3c972c7b52731cb12f678e25181680147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852aeffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042
    {
        "txid" : "d268e50f20480141ef2150e4b036197dc7aeaa4caf759ff3fd004034eff3093c",
        "version" : 1,
        "time" : 1412672622,
        "locktime" : 0,
        "unit" : "B",
        "vin" : [
            {
                "txid" : "9be0426ae843dd214b24e12d2f2f9aa8beae42710bfce33ae94988336aec3996",
                "vout" : 1,
                "scriptSig" : {
                    "asm" : "0 304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd35301 30450221008cd54b9d3a58d3b8cc37996016091cc657fdd0f605c765a721f4c61455eba2c5022042fb2133cc28243ca457e93f5645d34592c3c972c7b52731cb12f678e251816801 522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852ae",
                    "hex" : "0047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd353014830450221008cd54b9d3a58d3b8cc37996016091cc657fdd0f605c765a721f4c61455eba2c5022042fb2133cc28243ca457e93f5645d34592c3c972c7b52731cb12f678e25181680147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852ae"
                },
                "sequence" : 4294967295
            }
        ],
        "vout" : [
            {
                "value" : 50.00000000,
                "n" : 0,
                "scriptPubKey" : {
                    "asm" : "OP_DUP OP_HASH160 2ec6853a48d497ad2267f83f97abe1b595e1af66 OP_EQUALVERIFY OP_CHECKSIG",
                    "hex" : "76a9142ec6853a48d497ad2267f83f97abe1b595e1af6688ac",
                    "reqSigs" : 1,
                    "type" : "pubkeyhash",
                    "addresses" : [
                        "bGzbbVhQQRbQcDjTPxrcgifNh3dZjnpbUP"
                    ]
                }
            },
            {
                "value" : 49.99000000,
                "n" : 1,
                "scriptPubKey" : {
                    "asm" : "OP_HASH160 c39dbda222a630c5aeaff5fbd4d870d5e63d01ab OP_EQUAL",
                    "hex" : "a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab87",
                    "reqSigs" : 1,
                    "type" : "scripthash",
                    "addresses" : [
                        "buuCQmPMhMgB1txJRhsivhAxwgUUNVsoN1"
                    ]
                }
            }
        ]
    }

We can send it from any node:

    $ ./nud -unit=B sendrawtransaction 010000006eac3354019639ec6a338849e93ae3fc0b7142aebea89a2f2f2de1244b21dd43e86a42e09b01000000da0047304402206b9d5ce19a869ec5d9e8ceefcf8a5e9d7a9f34fda22ebe8b202f6e6d65af81b70220017119d50e7401bdbdccb522f9042bf4a08226f2814287146b12cef5984fd353014830450221008cd54b9d3a58d3b8cc37996016091cc657fdd0f605c765a721f4c61455eba2c5022042fb2133cc28243ca457e93f5645d34592c3c972c7b52731cb12f678e25181680147522102d4390de366895a81ea68fcf9b18725a0158350f0fc13b29daede56bf73ad58d321030e517111e415834a691197add91798b6c0933f4a369273e2c14b558e218acf9852aeffffffff0220a10700000000001976a9142ec6853a48d497ad2267f83f97abe1b595e1af6688acbca007000000000017a914c39dbda222a630c5aeaff5fbd4d870d5e63d01ab870000000042
    d268e50f20480141ef2150e4b036197dc7aeaa4caf759ff3fd004034eff3093c

The transaction was accepted in the blockchain: [d268e50f20480141ef2150e4b036197dc7aeaa4caf759ff3fd004034eff3093c](http://testnet.blockexplorer.nu/transactions/d268e50f20480141ef2150e4b036197dc7aeaa4caf759ff3fd004034eff3093c)
