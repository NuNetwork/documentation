---
title: Nu Client Commands
nav_heading: Technical Resources
filename: nu-client-commands.md
permalink: /nu-client-commands/
layout: kb
lang: en
callouts:
---

`nud [options] <command> [params]`
Send command to -server or nud

`nud [options] help`
List commands

`nud [options] help <command>`
Get help for a command

Command | Description
--------|------------
`-unit=S` | Pass the command to the NuShares RPC server
`-unit=B`| Pass the command to the NuBits RPC server
`-conf=<file>` | Specify configuration file (default: nu.conf)
`-pid=<file>` | Specify pid file (default: nud.pid)
`-gen` | Generate coins. DEPRECATED
`-gen=0` | Don't generate coins
`-min` | Start minimized
`-splash` | Show splash screen on startup (default: 1)
`-datadir=<dir>` | Specify data directory
`-dbcache=<n>` | Set database cache size in megabytes (default: 25)
`-dblogsize=<n>` | Set database disk log size in megabytes (default: 100)
`-timeout=<n>` | Specify connection timeout (in milliseconds)
`-proxy=<ip:port>` | Connect through socks4 proxy
`-dns` | Allow DNS lookups for addnode and connect
`-port=<port>` | Listen for connections on <port> (default: 7890 or testnet: 7895)
`-maxconnections=<n>` | Maintain at most <n> connections to peers (default: 125)
`-addnode=<ip>` | Add a node to connect to and attempt to keep the connection open
`-connect=<ip>` | Connect only to the specified node
`-listen` | Accept connections from outside (default: 1)
`-detachdb` | Detach block and address databases. Increases shutdown time (default: 0)
`-testnet` | Use the test network
`-debug` | Output extra debugging information
`-logtimestamps` | Prepend debug output with timestamp
`-printtoconsole` | Send trace/debug info to console instead of debug.log file
`-rpcuser=<user>` | Username for JSON-RPC connections
`-rpcpassword=<pw>` | Password for JSON-RPC connections
`-rpcport=<port>` | Listen for JSON-RPC connections on <port> (default: 14001 or testnet: 15001)
`-rpcallowip=<ip>` | Allow JSON-RPC connections from specified IP address
`-rpcconnect=<ip>` | Send commands to node running on <ip> (default: 127.0.0.1)
`-splitshareoutputs=<outputsize>` | Change the default 10,000 NuShares output size
`-blocknotify=<cmd>` | Execute command when the best block changes (%s in cmd is replaced by block hash)
`-upgradewallet` | Upgrade wallet to latest format
`-walletnotify=<cmd>` | Execute command when a wallet transaction changes (%s in cmd is replaced by TxID)
`-keypool=<n>` | Set key pool size to <n> (default: 100)
`-rescan` | Rescan the block chain for missing wallet transactions
`-checkblocks=<n>` | How many blocks to check at startup (default: 2500, 0 = all)
`-checklevel=<n>` | How thorough the block verification is (0-6, default: 1)
`-rpcssl` | Use OpenSSL (https) for JSON-RPC connections
`-rpcsslcertificatechainfile=<file.cert>` | Server certificate file (default: server.cert)
`-rpcsslprivatekeyfile=<file.pem>` | Server private key (default: server.pem)
`-rpcsslciphers=<ciphers>` | Acceptable ciphers (default: TLSv1+HIGH:!SSLv2:!aNULL:!eNULL:!AH:!3DES:@STRENGTH)
`-upnp` | Use Universal Plug and Play to map the listening port (default: 0)
`-?` | This help message

### ifdef QT_GUI

Command | Description
--------|------------
`-server` | Accept command line and JSON-RPC commands
`-lang=<lang>`  | Set language, for example \"de_DE\" (default: system locale)
`-dnsseed`  | Find peers using DNS lookup (default: 1)
`-banscore=<n>` | Threshold for disconnecting misbehaving peers (default: 100)
`-bantime=<n>` | Number of seconds to keep misbehaving peers from reconnecting (default: 86400)
`-maxreceivebuffer=<n>` | Maximum per-connection receive buffer, <n>\*1000 bytes (default: 10000)
`-maxsendbuffer=<n>` | Maximum per-connection send buffer, <n>\*1000 bytes (default: 10000)

### if USE_UPNP

Command | Description
--------|------------
`-upnp` | Use Universal Plug and Play to map the listening port (default: 1)


### ifdef WIN32

Command | Description
--------|------------
`-printtodebugger` | Send trace/debug info to debugger

### if !defined(WIN32) && !defined(QT_GUI)

Command | Description
--------|------------
`-daemon` | Run in the background as a daemon and accept commands
