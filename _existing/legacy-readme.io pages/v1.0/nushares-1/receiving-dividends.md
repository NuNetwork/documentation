#Instructions for how to set up your connection between Peer(coin/unity) and Nu

Dividends are sent out in the form of Peercoins. Once you export the Peercoin keys from your Nu wallet into your Peer(coin/unity) wallet the dividends will be accessible. Follow the instructions below to export the keys.

Make sure that for both Nu and your Peer(coin/unity) wallet client that you have a [configuration file](http://docs.nubits.com/v1.0/docs/creating-conf-file) available, and that each has at a minimum the following information.
[block:code]
{
  "codes": [
    {
      "code": "  server=1\n  rpcuser={anything}\n  rpcpassword={anything}\n  // for use on the testnet, include `testnet=1`",
      "language": "shell"
    }
  ]
}
[/block]
  * Once the configuration files are in place, launch both clients.
  * Go back to your Nu wallet and change your units to work from the NuShares side (file menu: Unit > NuShares).
  * From the file menu: Shares > Export Peercoin keys

If everything works as expected, you will see a dialog appear with a count of the number of addresses that have been exported. You can confirm this action by viewing your Peercoin wallet and looking on the "Receive Coins" tab. There should be a number of new addresses with the label "NuShares" that match the number that was exported in the previous step. If you do not see this, please make sure that your wallet was unlocked (and not just unlocked for minting) and try it again.
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/nsN7NfNTQ7edSTl3kFX0",
        "ExportingKeysNow.png",
        "315",
        "128",
        "#374773",
        ""
      ]
    }
  ]
}
[/block]
In your Peercoin wallet client, on the Receiving tab, you will see that the NuShares dividend addresses have been included:
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/L5Xwq7goRcyVrmlFpVKC",
        "PeercoinWallet.png",
        "860",
        "581",
        "#324166",
        ""
      ]
    }
  ]
}
[/block]

Once that has been completed, you'll be ready for a dividend distribution. If you should add additional NuShares addresses in the future, please make sure you follow the same steps again to integrate those new paired keys into your Peercoin wallet. You will not duplicate existing keys, so this operation can be run as many times as you need, into the future.
[block:api-header]
{
  "type": "basic",
  "title": "Troubleshooting"
}
[/block]
#0 key(s) were exported to Peercoin

If you see a dialog like this, when you try to export the keys:
[block:image]
{
  "images": [
    {
      "image": [
        "https://www.filepicker.io/api/file/JJr9mVBvQYqBZvRrfoTl",
        "keyExport.png",
        "326",
        "145",
        "#35487a",
        ""
      ]
    }
  ]
}
[/block]
You have probably already exported the keys to your client. Check your Peer(coin/unity) client to see if the keys exist.

##Port conflicts

If you experience problems with connecting the two wallets, please confirm that your network allows traffic on the following ports:
[block:code]
{
  "codes": [
    {
      "code": "PROTOCOL PORT  7890\nRPC PORT  14001     // Base RPC port used by the NuShares RPC server. Other unit RPC servers listen on RPC_PORT+1, RPC_PORT+2, etc.\nRPC PORT  14002     // NuBits\n\n// Same rules apply to testnet, but on different ports\nTESTNET PORT   7895\nTESTNET RPC PORT  15001     // NuShares\nTESTNET RPC PORT  15002     // NuBits\n\n// Peercoin ports used when communicating with the Peercoin wallet for dividend distributions\nPEERCOIN RPC PORT  9902\nPEERCOIN TESTNET RPC PORT  9904",
      "language": "text"
    }
  ]
}
[/block]