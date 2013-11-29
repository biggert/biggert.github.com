---
layout: post
title: "Copy and paste to Visual Studio ASP.NET page from SQL Management Studio"
description: ""
category: ""
tags: [SQL,ASP]
---
{% include JB/setup %}

As I'm bringing over some older posts from my previous blog, I thought this one might be helpful to some (notice I was using VS2005 at the time but this also works for VS2008).

So I was doing some grunt work of making a few textboxes which will be filled from a SQL table from a remote database. I decided to pop open SQL Management Studio in my second monitor and copy the field names straight from the table and paste them onto the ASP.Net page. I clicked on a field name and unknowingly left the whole row selected, hit CTRL-C, and then pasted right into the ASP.Net page. To my surprise, a Gridview showed up and its related datasource. Also, connection string was added to my Web.config. I was not aware of this functionality at all but I thought I’d post it as it could save some time for a few people.

1. With Visual Studio 2005 .NET open to an ASPX page, open SQL Management Studio.
2. Right click on the table you want to create a Gridview with and select ‘Design’.
3. Highlight the field(s) you want to show in the Gridview (use shift-select for multiples).
4. Press CTRL-C to copy to the clipboard.
5. Place the cursor in the ASPX page where you want the Gridview to appear and press CTRL-V.
6. That’s it! You will have a simple Gridview with the fields you selected, a SqlDataSource underneath it, and a connection string in your Web.Config.

Here’s an example of the resulting ASPX output:
<pre name="code" class="html">
&lt;asp:GridView ID="GridView1" runat="server" DataSourceID="SqlDataSource2"
EmptyDataText="There are no data records to display." AutoGenerateColumns="False"&gt;
&lt;Columns&gt;
&lt;asp:BoundField DataField="Processor" SortExpression="Processor" HeaderText="Processor"&gt;&lt;/asp:BoundField&gt;
&lt;asp:BoundField DataField="MinAmount" SortExpression="MinAmount" HeaderText="MinAmount"&gt;&lt;/asp:BoundField&gt;
&lt;asp:BoundField DataField="Requestor" SortExpression="Requestor" HeaderText="Requestor"&gt;&lt;/asp:BoundField&gt;
&lt;asp:BoundField DataField="OutputFilesPath" SortExpression="OutputFilesPath"
HeaderText="OutputFilesPath"&gt;&lt;/asp:BoundField&gt;
&lt;/Columns&gt;
&lt;/asp:GridView&gt;
&lt;asp:SqlDataSource ID="SqlDataSource1" runat="server" SelectCommand="SELECT [Processor],
 [MinAmount], [Requestor], [OutputFilesPath] FROM [tbl_Settings]”
ConnectionString=”&lt;%$ ConnectionStrings:MPConnectionString1 %&gt;”
ProviderName=”&lt;%$ ConnectionStrings:MPConnectionString1.ProviderName %&gt;”&gt;
&lt;/asp:SqlDataSource&gt;
</pre>
