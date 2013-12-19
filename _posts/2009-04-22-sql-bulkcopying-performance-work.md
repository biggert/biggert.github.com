---
layout: post
title: "SQL Bulkcopying performance work"
description: ""
category: ""
tags: [SQL,C#]
---
{% include JB/setup %}
Some of my time spent in application performance tuning around out SQL backend products is reviewing code that could otherwise be performed on the SQL server with much faster results. Over the years, I've spent a lot of time with .NET's SQLBulkCopy and SQLXML BulkLoad. I've spent countless hours scheming up new ways to get our data processing techniques out of  un-scalable C# code of row by row (or chunks) processing of the data and into the blazing fast world that is SQL BulkCopy/BulkLoad.

One recent opportunity arose where we literally had a piece of C# code iterating row after row, performing some crazy logic, and then copying data from one table to another, and throwing around some more logic and performed updates back on the 2 tables. To be a little more specific, we had a table full of filenames in a certain format and we needed to copy this data into a separate table with more metadata about the filenames. We then wanted to copy some data from this table to yet another table. Very generic statements I know but this isn't exactly an open source product.

This code block took over 3 hours to run for a measly 10,000 rows. We applied a few BulkCopies and were very happy with the results. We actually added code to dynamically create a working table (I want to avoid the word "temp table" since it is not a true SQL temp table but in the scope of the application, since it is added and removed, it is a "temp table"). With this working table, we could then convert the C# Logic to logic performed in a SELECT statement which also prevents UPDATE statements from being executed so that this can be an INSERT only (much faster in the SQL world). So finally, we converted a couple hundred lines of C# code to 3 BulkCopies (1 for the working table, 2 for our tables). All the logic is performed in 3 SELECT statements optimized to their fullest (dirty reads where possible, LEFT JOINs instead of IN/NOT IN, limited subqueries, etc.).

Overall, in the grand scheme of things, to be fair, the complete process of some of which is not mentioned here took about a thousand lines of code which took over 3 hours to run for 10,000 rows to 5 bulkcopies using 3 working tables and the result is over 100,000 rows takes 3 seconds. Three seconds... to be fair with a direct comparison, the original 10,000 rows takes 2 seconds, most of which is spent creating the "temporary working tables" or opening the SQL connection/SQL DataReaders. Awesome stuff!