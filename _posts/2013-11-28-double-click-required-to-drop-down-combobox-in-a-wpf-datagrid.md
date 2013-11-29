---
layout: post
title: "Double click required to drop down ComboBox in a WPF DataGrid"
description: ""
category: ""
tags: [WPF,C#]
---
{% include JB/setup %}

Just a quick post... I had this problem in .NET 4.0 WPF DataGrid where the user had to double-click (select the cell then interact with the control) a combobox (drop down list) within a DataGrid to view the contents of it. After doing some research, I found posts about how this affects checkboxes in datagridcells. In my case, I have a DataGridTemplateColumn that has a ComboBox in it. On that Combobox, I set the following:

<pre lang="XAML">&lt;ComboBox IsDropDownOpen="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type DataGridCell}}, Path=IsEditing}" SelectedValue="{Binding Mode=TwoWay, Path=SourceFieldName}"...</pre>

And all is well... single-click to drop it down.