---
layout: post
title: Setting up StackExchange's Opserver
date: '2013-10-25T19:36:00.002-04:00'
author: Pat Hyatt
tags:
- Nick Craver
- StackOverflow
- StackExchange
- .NET
- Opserver
- C#
- exception
- monitoring
modified_time: '2013-10-25T19:38:16.860-04:00'
thumbnail: http://2.bp.blogspot.com/-vb_mZnUqkbg/Umr5EG_0qxI/AAAAAAAAAlU/NqRWLyaC9nk/s72-c/blog_redis.png
blogger_id: tag:blogger.com,1999:blog-1130780247100205939.post-6230668647083139269
blogger_orig_url: http://patpack.blogspot.com/2013/10/setting-up-stackexchanges-opserver.html
---

<a href="http://nickcraver.com/blog/">Nick Craver</a> from <a href="http://stackexchange.com/">StackExchange</a> recently posted StackExchange's homegrown monitoring system.  The system, named <a href="https://github.com/opserver/Opserver">Opserver </a>is available on <a href="http://github.com/">GitHub</a>.

In this post I hope to gloss over some of the issues and/or configuration steps necessary to run this slick monitor.
So lets try this.

<h3>Installation:</h3>
<ol>
	<li>
		Grab the code from GitHub either, for the lazy here is the <a href="https://github.com/opserver/Opserver/archive/master.zip">zip file link</a>
	</li>
	<li>
		If using Visual Studio 2010 or previous, make sure you have ASP.NET MVC installed. Grab that <a href="http://www.asp.net/mvc/mvc4">here</a> and make sure to run the installer as administrator [Windows 7+].
	</li>
	<li>
		Crack open the solution file (either from your cloned repo OR the unzipped package downloaded in step ). There should be 2 projects visible and loaded. If you get a "The project file '.....csproj' cannot be opened. The project type is not supported by this installation." error, see this <a href="http://stackoverflow.com/questions/1531120/asp-net-mvc-project-not-supported-by-this-installation#1532183">StackOverflow answer</a>.
	</li>
	<li>
		Compile. You should have no errors and everything succeeds.
	</li>
</ol>

<div>
	<i>Side note</i>: This codebase was built using Visual Studio 2012 and recently updated to use Visual Studio 2013.
</div>

<h3>Configuration:</h3>
<div>
	All configuration is handled by .json files in the Opserver/Config directory. Nick has a .example file for each of the different types of dashboards there are. Some of these appear to be very centric to StackExchanges build, so out of the box you may not be able to use all the configurations without reworking some areas of your codebase.
</div>
<h3>SecuritySettings.json</span></h3>
<div>
	This is the first file you'll need to copy/paste in order to get into the system.
</div>
<div>
	Edit this file to match the security settings you want.
</div>
<div>
	The example looks like this:
</div>

```xml
	<?xml version="1.0" encoding="utf-8"?>
	<SecuritySettings provider="AD">
	 <!-- Optional, these networks can see the overview dashboard without authentication -->
	    <InternalNetworks>
	        <Network name="SE Internal" cidr="10.0.0.0/8" />
	    </InternalNetworks>
	</SecuritySettings>
	 
	<!-- Example of global access for everyone:<SecuritySettings provider="alladmin" />-->
```

which limits access to StackExchange's internal network, yours will need to be changed


<div>
	Possible "provider" attributes are: "activedirectory", "ad", "alladmin", or no attribute in which everyone is read only. "ad" and "activedirectory" are analogous.
</div>

<div>
	For my case I have everyone being an admin, since this is mainly for our internal development and QA teams.
</div>

<div>
	Mine looks like this:
</div>

```xml
<?xml version="1.0" encoding="utf-8"?>
<SecuritySettings provider="alladmin">
</SecuritySettings> 
```


Note, even if everyone is an admin, they will have to login initially using an empty username/password combination to get into the system.

<h3>RedisSettings.json</h3>
<div>
	If you do not know what Redis is or do not use it skip this.
</div>

<div>
	Adding a RedisSettings.json file allows you to monitor Redis memory use as well as perform some health checks.
</div>

<div>
	The configuration for Redis is a tad cryptic for me still, so bear with me.
</div>

<div>
	Here is our config file, modified to remove server names and specifics:
</div>

```json
{
 "allServers": {
  "name": "All",
  "instances": [
   {
    "name": "Core",    
    "analysisRegexes": {
     "**Dev**": "^dev-",
     "**Live**": "^prod-",
    }
   }   
  ]
 },
 "Servers": [
  { "name": "server1" },
  { "name": "server1Slave1" },
  { "name": "server2" },
  { "name": "server2Slave1" },
  { "name": "server2Slave2" }
 ]
}
```

<div>
	Under the instances array we have a "Core" name and two children that define regular expressions to match Redis key names for categorizing. That is, if a key starts with "dev-", it will be categorized as "**Dev**" under the "Core" instance when running analysis.
	The Servers array defines the server names your Redis instances are running on.
</div>

<div>
	Here's a screenshot of what the Redis monitor home page looks like:
	<br />
	<a href="http://2.bp.blogspot.com/-vb_mZnUqkbg/Umr5EG_0qxI/AAAAAAAAAlU/NqRWLyaC9nk/s1600/blog_redis.png">
		<amp-img height="92" src="http://2.bp.blogspot.com/-vb_mZnUqkbg/Umr5EG_0qxI/AAAAAAAAAlU/NqRWLyaC9nk/s400/blog_redis.png" width="400" />
	</a>
</div>

<div>
	You can see the "Core" name in use on the left.
</div>

<h3>SQLSettings.json</h3>The entries in this file define the connection strings for any SQL server instances you wish to monitor. There are two main arrays to populate, "clusters" and "instances".</h3>

<div>
	"clusters" refers to SQL Server 2012 cluster configurations. If the SQL instance you put in here are not SQL Server 2012 you can get memory use spark charts only. Outside of that it will appear offline.
</div>

<div>
	"instances" refers to standalone SQL server instances, and at least in our internal setup, make up a majority of our SQLSettings configuration.
</div>

<div>
	Our configuration, truncated some for brevity:
</div>


```json
{
    "defaultConnectionString": "Data Source=$ServerName$;Initial Catalog=master;Integrated Security=SSPI;",
    "clusters": [
        {
         "name": "SDCluster01",
         "nodes": [
          { "name": "SDCluster01\\SDCluster01_01" },
   { "name": "SDCluster02\\SDCluster01_02" },
         ]
        },       
    ],
    "instances": [        
        { "name": "SDDB01" },
 { "name": "SDDB02" },
 { "name": "SDDB03" },
 { "name": "SDDB04" },
    ]
}
```

<div>
	Any one of the JSON objects that have a "name" property, can also specify a "connectionString" entry in case it differs from the "defaultConnectionString"'s entry.
</div>
<div>
	Here is a display of our non 2012 cluster and information:
</div>

<div>
	<a href="http://1.bp.blogspot.com/-mCUf9nkdEyU/Umr9z6sg7GI/AAAAAAAAAlg/sK3xXOjIQ9c/s1600/blog_sql.png">
		<amp-img height="207" src="http://1.bp.blogspot.com/-mCUf9nkdEyU/Umr9z6sg7GI/AAAAAAAAAlg/sK3xXOjIQ9c/s400/blog_sql.png" width="400" />
	</a>
</div>

<div>
	As you can see, the top "cluster" is highlighted in red, even tho the spark chart is coming in.
</div>
<div>
	Also you can see under the standalone grouping we have 1 instance that's not up at all.
</div>
<div>
	Each one of these instances you can drill into to obtain more detailed information, for example:
</div>
<div>
	<a href="http://4.bp.blogspot.com/-HDk9FmYdorM/Umr-cHnXn9I/AAAAAAAAAlo/XDLQbBdh7DI/s1600/blog_sql2.png">
		<amp-img height="288" src="http://4.bp.blogspot.com/-HDk9FmYdorM/Umr-cHnXn9I/AAAAAAAAAlo/XDLQbBdh7DI/s400/blog_sql2.png" width="400" />
	</a>
</div>

<h3>ExceptionsSettings.json</h3>
<div>
	To use this monitor panel, you pretty much need to use <a href="https://github.com/NickCraver/StackExchange.Exceptional">StackExchange.Exceptional</a>. This, again, is StackExchange's error logging system, which writes unhandled exceptions to a central database.
</div>

<div>
	If you happen to not use this, skip this for now.
	The configuration for this is pretty straight forward for a quick setup, the only necessary item is the connection string of the database your Exceptional logging system is writing to.
</div>

```json
{
    "warningRecentCount": "100",
    "criticalRecentCount": "200",
    "viewGroups": "StatusExceptionsRO",
    "applications": [
        "Core",  
        "Customer Support",
        "API",
        "Intranet",
        "Polling"
    ],
    "stores": [
        {
            "name": "SanDiego",
            "queryTimeoutMs": 2000,
            "pollIntervalSeconds": 10,
            "connectionString": "Server=SDDB_01;Database=Exceptions;Integrated Security=SSPI;"
        }
    ]
}
```


<div>
	String items underneath "applications" defines what is displayed by default on the Exception pages header. If an exception is written to the database that does not fit any of those application names, a new category will display in the pane.
</div>

<div>
	I was going to post a screenshot, but after blurring out anything from our stack, it was useless. I would like to add however, that both Exceptional and the Exception page are just beautiful.
</div>

<div>

<h3>Conclusion</h3>
<div>
	So far my coworkers and I love this, and I can see from the code its only getting better (hello there sp_WhoIsActive, sp_BlitzIndex!).
</div>

<div>
	I hope this helps someone. Together with Exceptional I've personally found 3 issues with our codebase not previously known, scary but also eye opening. And I think that is the goal, make your errors eye opening and easy to see, so you can fix them.
</div>