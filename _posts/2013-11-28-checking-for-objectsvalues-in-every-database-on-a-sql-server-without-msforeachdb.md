---
layout: post
title: "Checking for objects/values in every database on a SQL server without msforeachdb"
description: ""
category: ""
tags: [SQL]
---
{% include JB/setup %}

Recently, I needed to iterate through every database on a SQL server in order to determine whether it matched a certain schema I needed basically checking for the existence of a table in my case. For years I've used msforeachdb but we recently had some reports of unexpected behavior with this stored procedure where it would just completely skip a database or two... so throwing that out the window I came across another option here: <a href="http://blogs.lessthandot.com/index.php/DataMgmt/DataDesign/how-to-get-information-about-all-databas">http://blogs.lessthandot.com/index.php/DataMgmt/DataDesign/how-to-get-information-about-all-databas</a>

&nbsp;

To be more specific about the scenario I needed to use this in, I simply wanted to know if 2 or more databases existed with the desired schema so the query I came up with is here:

&nbsp;

Use the information on this page, I came up with this query:
<pre lang="sql">DECLARE @SQL NVARCHAR(MAX)
SELECT @SQL = COALESCE(@SQL,'') + '
BEGIN TRY
IF ((SELECT @COUNT) &lt; 2)
BEGIN
select @COUNT = @COUNT + COUNT([TABLE_CATALOG]) from ' + QUOTENAME(name) + '.INFORMATION_SCHEMA.Tables WHERE [TABLE_NAME] = ''MyTable'' AND [TABLE_TYPE] = ''BASE TABLE'';
END
ELSE
BEGIN
SELECT @COUNT;
RETURN;
END;
END TRY
BEGIN CATCH
--Do noting as we don''t care for non-DB access issues but don''t want to quit
END CATCH
'
FROM sys.databases
ORDER BY name
SELECT @SQL = 'DECLARE @count int; SET @count = 0;' + @SQL
EXECUTE(@SQL)</pre>
&nbsp;

So with that we've got a quick and dirty SQL statement that simply checks each database for the occurence of MyTable. If 2 or more databases have that object, we return the number and bail.

&nbsp;

Now we don't have to rely on an undocumented stored procedure to get the job done.