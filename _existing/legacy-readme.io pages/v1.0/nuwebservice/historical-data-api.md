[block:api-header]
{
  "type": "basic",
  "title": "Data API Introduction"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Do not use beta software in production",
  "body": "This API is a temporary beta and we advise not to use it in production environment. While we work towards a production-ready API, you can use this for toy projects and experiments."
}
[/block]
We have put together a temporary HTTP service to access historical data about the Nu Network.  A python script updates the database each time a new block is found, and updates the *getliquidityinfo* every 30 seconds. 
[block:callout]
{
  "type": "info",
  "body": "The first available data-points are dated 2014-10-17 12:05:58. The data format is reported as *json* raw data, as returned from the Nu daemon."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Data API overview"
}
[/block]
Base URL : http://nu.mj2p.co.uk/ 

Parameters : The API accepts three GET parameters 
[block:parameters]
{
  "data": {
    "h-0": "Parameter Name",
    "0-0": "cmd",
    "1-0": "frm",
    "2-0": "to",
    "h-1": "Parameter Description",
    "0-1": "the name of the command to retrieve",
    "1-1": "the date of the earliest value",
    "h-2": "Parameter format",
    "0-2": "see list of available commands below",
    "1-2": "YYYY-MM-DD%20hh:mm:ss",
    "2-2": "YYYY-MM-DD%20hh:mm:ss",
    "2-1": "the date you want return data up to"
  },
  "cols": 3,
  "rows": 3
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "List of available commands"
}
[/block]

  * getinfo 
  * getcustodianvotes
  * getdifficulty
  * getmotions 
  * getparkrates
  * getpeerinfo
  * getrawmempool
  * getvote.
  * getliquidityinfo
  * getparkvotes
[block:api-header]
{
  "type": "basic",
  "title": "API usage Examples"
}
[/block]
  * Retrieve historical liquidity info specifying the time-range: 
  http://nu.mj2p.co.uk/nu-data?cmd=getliquidityinfo&frm=2014-10-18%2008:35:00&to=2014-10-18%2008:36:00
  * Retrieve historical *getpeerinfo* using smaller timestamps as 'frm' and 'to' : http://nu.mj2p.co.uk/nu-data?cmd=getpeerinfo&frm=2014-10-18&to=2014-10-19
  * Retrieve all historical *getcustodianvotes* datapoints available http://nu.mj2p.co.uk/nu-data?cmd=getcustodianvotes