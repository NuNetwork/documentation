---
title: Create your own Nu DNS seed with CloudFlare 
nav_heading: Technical Resources
filename: create-dns-seed.md
permalink: /create-nu-dns-seed/
layout: kb
lang: en
callouts:
  - shortname: beta
    type: warning
    title: Do not use beta software in production
    body: This software is in beta-status and we advise you to use it with caution.
---
## Introduction 
This tutorial will show you how to run your own DNS seed. 

It will describe how you can achieve this using nubits-seeder and cf-php. 

Nubits-seeder is a small crawler, that checks for live nodes on NuNet.
Cf-php is a script which queries the CloudFlare API and enters the seed nodes crawled by nubits-seeder into the DNS zone file. 

You can find the repo for both programs here: [https://github.com/bananenwilly/nubits-seeder]

We will not talk much about nubits-seeder in this tutorial. Cf-php is where the magic happens.  

## What does cf-php do?

It reads a file called dnsseed.dump in the nubits-seeder root directory, which is continuously created when nubits-seeder is crawling for nodes. 
It will generate an IP-table from the dnseed.dump file and pushes this table to a CloudFlare (CF) enabled domain of your choice over the Cloudflare API.

A DNS zone file created by cf-php will look something like this:

```
;; ANSWER SECTION:
nuseed.coinerella.com. 299 IN A 212.129.19.120
nuseed.coinerella.com. 299 IN A 217.23.13.138
nuseed.coinerella.com. 299 IN A 162.243.108.181
nuseed.coinerella.com. 299 IN A 188.226.223.94
nuseed.coinerella.com. 299 IN A 85.214.145.24
nuseed.coinerella.com. 299 IN A 104.131.41.17
nuseed.coinerella.com. 299 IN A 176.9.65.41
nuseed.coinerella.com. 299 IN A 176.9.113.75
nuseed.coinerella.com. 299 IN A 73.7.110.25
nuseed.coinerella.com. 299 IN A 212.114.48.31
```

There is no need for you to run your own DNS server. It's using the DNS servers provided by CloudFlare. 

## Requirements
  * `CloudFlare.com account`
  * `Domain (e. g. praisejordanleeourlordandsaviour.com) configured to use CF's DNS servers`
  * `small server (Raspberry Pis can easily handle this)`
  * `php5-cli, php5-curl, nubits-seeder repo`

## Let's get started

  * `Get your CF API Key (CloudFlare.com -> My Settings -> Account -> API Key -> View API Key) and have it ready`
  * `install php5-cli and php5-curl`
  * `Download and start nubits-seeder`

```shell
git clone https://github.com/bananenwilly/nubits-seeder
cd nubits-seeder
make
chmod +x dnsseed
./dnsseed
or
screen -dmS nuseed sh -c "./dnsseed"
to have a screen session, detach the screen session with CTRL+A+D
```

  * `Open cf-php/cf.php in an editor of your choice and edit the config paramters accordingly.`

```php
$domain ="domain.com";
$name = "nuseed"; //subdomain e.g. name.domain.com 
$number_of_records = 10; //maximum n A records with $name... 10 is recommended
$user = "emailofcloudflareaccount"; //user name
$key = "yourapikey"; //key for cloudflare api found in account settings
$seed_dump = "/path/to/dnsseed.dump"; //absolute path to dnsseed.dump in the nubits-seeder root directory
```

  * `Have a cronjob run cf-php regularly`
```
crontab -e
* * * * * php ~/nubits-seeder/cf-php/cf.php
```

This will run the cf.php script every minute. 

That should be it. You now have your own Nu DNS seed. 
