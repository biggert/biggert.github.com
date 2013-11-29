---
layout: post
title: "Another good benefit of using Application Name in a connection string"
description: ""
category: ""
tags: [C#,SQL]
---
{% include JB/setup %}

I've seen a plethora of posts like <a href="http://johnnycoder.com/blog/2006/10/24/take-advantage-of-application-name/">this one</a> which mention the benefits of using "Application Name" in your connection string. I thought I'd add on to this another neat item that people could use. While it isn't exactly reinventing the wheel, the technique is commonly forgotten about. We use it in WayPoint since it can run multiple imports into a CaseLogistix library (SQL database) at the same time.

So, first we add the "Application Name" to the SQL connection string but we append a GUID to the end of it (to make sure it's unique). Then, if our application needs to be aware of multiple instances connected to the same SQL database, we simply run this query:

<pre name="code" class="sql">
select count(*) from master.dbo.sysprocesses JOIN master.dbo.sysdatabases ON
master.dbo.sysprocesses.dbid = master.dbo.sysdatabases.dbid
where IsNull(program_name, '') &lt;&gt; ''
AND program_name like 'WayPoint-%'
AND program_name &lt;&gt; 'WayPoint-&lt;%% Our current GUID here %%&gt;'
AND master.dbo.sysdatabases.name = '&lt;%% Our current database name %%&gt;'
</pre>

This tells us the count of processes of other WayPoints running. Even better, we can dive further into this query to get info about the other processes and even kill them off if needed or do whatever with them. Not rocket science but a good thing to have in your back pocket if you need it.