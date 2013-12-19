---
layout: post
title: "A few good custom WPF controls found along the way"
description: ""
category: ""
tags: [C#,WPF]
---
{% include JB/setup %}

So in my work with WPF, I've needed either controls to supplement what was missing from Winforms or simply to match up with the current user experience's of today's application. I take no credit in actually developing these controls, just finding them on the web via Google. FYI - this article was written on .NET 3.5 as I know some of these will be included with .NET 4.0 WPF.

Linklabel:
http://www.blagoev.com/Blog/post/Building-a-WPF-LinkLabel-control.aspx

NOTE: I highly recommend properly binding the IsEnabled property in the Style. If you don't, having the IsEnabled property set to false on initial load and then changing it later will not properly enable the control.
To be more specific, add the highlighted line in the Template setter:
```xml
<Hyperlink
x:Name="PART_InnerHyperlink"
NavigateUri="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Url}"
Style= "{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=HyperlinkStyle}"
Command="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Command}"
CommandParameter="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=CommandParameter}"
CommandTarget="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=CommandTarget}"
IsEnabled="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=IsEnabled}"/>
<local:BindableRun
BoundText="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Content}"/>
</Hyperlink>
```
SearchTextBox:
http://davidowens.wordpress.com/2009/02/18/wpf-search-text-box/

WPF Datagrid (I'm sure you know about this one):
http://www.codeplex.com/wpf

Splitbutton (Couple different flavors here):
http://anothersplitbutton.codeplex.com
http://www.codeproject.com/KB/WPF/WpfSplitButton.aspx
http://blogs.msdn.com/llobo/archive/2006/10/25/Split-Button-in-WPF.aspx
http://wpfsplitbutton.codeplex.com

Closeable Tab:
http://geekswithblogs.net/kobush/archive/2007/04/08/CloseableTabItem.aspx

Loading animation (I find that using the base is fine but making these your own is pretty easy):
http://social.msdn.microsoft.com/forums/en-US/wpf/thread/0875ebf8-bb77-45ea-a929-d40743a3bf03/
http://chriscavanagh.wordpress.com/2008/07/25/improved-xaml-loading-animation/
http://brianlagunas.com/2009/08/21/a-simple-wpf-loading-animation/

DockPanelSplitter (added this after the post as I found it the same day, amazingly helpful control):
http://www.codeproject.com/KB/WPF/DockPanelSplitter.aspx

FYI - if any of these links are down, please let me know and I'll either update the link.

UPDATE: Fixed the Linklabel link to actually point to the place it stated. Oops
