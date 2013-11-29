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
<a href="http://www.blagoev.com/Blog/post/Building-a-WPF-LinkLabel-control.aspx" target="_blank">http://www.blagoev.com/Blog/post/Building-a-WPF-LinkLabel-control.aspx</a>

NOTE: I highly recommend properly binding the IsEnabled property in the Style. If you don't, having the IsEnabled property set to false on initial load and then changing it later will not properly enable the control.
To be more specific, add the <span style="color: #ff0000;">highlighted </span>line in the Template setter:
<p style="padding-left: 30px;">&lt;Hyperlink
x:Name="PART_InnerHyperlink"
NavigateUri="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Url}"
Style= "{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=HyperlinkStyle}"
Command="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Command}"
CommandParameter="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=CommandParameter}"
CommandTarget="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=CommandTarget}"
<span style="color: #ff0000;">IsEnabled="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=IsEnabled}"</span>&gt;
&lt;local:BindableRun
BoundText="{Binding RelativeSource= {RelativeSource TemplatedParent}, Path=Content}"/&gt;
&lt;/Hyperlink&gt;</p>
SearchTextBox:
<a href="http://davidowens.wordpress.com/2009/02/18/wpf-search-text-box/" target="_blank">http://davidowens.wordpress.com/2009/02/18/wpf-search-text-box/</a>

WPF Datagrid (I'm sure you know about this one):
<a href="http://www.codeplex.com/wpf" target="_blank">http://www.codeplex.com/wpf</a>

Splitbutton (Couple different flavors here):
<a href="http://anothersplitbutton.codeplex.com/" target="_blank">http://anothersplitbutton.codeplex.com/</a>
<a href="http://www.codeproject.com/KB/WPF/WpfSplitButton.aspx" target="_blank">http://www.codeproject.com/KB/WPF/WpfSplitButton.aspx</a>
<a href="http://blogs.msdn.com/llobo/archive/2006/10/25/Split-Button-in-WPF.aspx" target="_blank">http://blogs.msdn.com/llobo/archive/2006/10/25/Split-Button-in-WPF.aspx</a>
<a href="http://wpfsplitbutton.codeplex.com/" target="_blank">http://wpfsplitbutton.codeplex.com/</a>

Closeable Tab:
<a href="http://geekswithblogs.net/kobush/archive/2007/04/08/CloseableTabItem.aspx" target="_blank">http://geekswithblogs.net/kobush/archive/2007/04/08/CloseableTabItem.aspx</a>

Loading animation (I find that using the base is fine but making these your own is pretty easy):
<a href="http://social.msdn.microsoft.com/forums/en-US/wpf/thread/0875ebf8-bb77-45ea-a929-d40743a3bf03/" target="_blank">http://social.msdn.microsoft.com/forums/en-US/wpf/thread/0875ebf8-bb77-45ea-a929-d40743a3bf03/</a>
<a href="http://chriscavanagh.wordpress.com/2008/07/25/improved-xaml-loading-animation/" target="_blank">http://chriscavanagh.wordpress.com/2008/07/25/improved-xaml-loading-animation/</a>
<a href="http://brianlagunas.com/2009/08/21/a-simple-wpf-loading-animation/" target="_blank">http://brianlagunas.com/2009/08/21/a-simple-wpf-loading-animation/</a>

DockPanelSplitter (added this after the post as I found it the same day, amazingly helpful control):
<a href="http://www.codeproject.com/KB/WPF/DockPanelSplitter.aspx" target="_blank">http://www.codeproject.com/KB/WPF/DockPanelSplitter.aspx</a>

FYI - if any of these links are down, please let me know and I'll either update the link.

UPDATE: Fixed the Linklabel link to actually point to the place it stated. Oops