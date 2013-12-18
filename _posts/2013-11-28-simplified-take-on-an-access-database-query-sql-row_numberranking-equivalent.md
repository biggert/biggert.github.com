---
layout: post
title: "Simplified take on an Access Database query SQL 'ROW_NUMBER'/ranking equivalent "
description: ""
category: ""
tags: [Access,SQL]
---
{% include JB/setup %}

Earlier this week I needed the ability to write a query in an Access Database similar to the functionality provided by MSSQL's ROW_NUMBER (OVER ...) keyword. It took some thought and a little googling and wasn't apparenty even though there were a few examples out there but they were kinda muddied up and not obvious (too much extra crap) so I thought I'd provide a simpler version here. So in my case, I just needed to read from a table with unknown rows a list of names... but I needed a unique identifier for each name (row) which I could use with an incrementing integer. While I did have an ID column available, it couldn't be depended on to be sequential due to deletes that may have occurred.

The resulting Access query is this:
```sql
SELECT [Name],
(SELECT Count([ID]) AS C
FROM [tblNames] AS A
WHERE A.[ID] > [tblNames].[ID]) AS [Row]
FROM [tblIssues]
```
From this, I can add a WHERE clause like 'WHERE \[Row\] = 0', 'WHERE \[Row\] = 1', etc. to specifically get each individual name from the table. Nice and easy (and more readable logic than most of the examples I found out there).
