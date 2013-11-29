---
layout: post
title: "WPF Datagrid and the dreaded double tab focus issue"
description: ""
category: ""
tags: [C#]
---
{% include JB/setup %}

So I just had to figure this out on my own over the last hour or so and found it to be a good candidate for a post. I found my path through the internet on this one but apparently everyone's solution didn't exactly equal to mine for some reason or another. So here we go:

<strong><span style="text-decoration: underline;">Problem</span></strong>

When using a DataGridTemplateColumn from the DataGrid in the <a href="http://www.codeplex.com/wpf">WPF Toolkit</a> in .NET 3.5 (after attending PDC09, I know .NET4 will have a built-in WPF DataGrid), if you want to simply use tab to change the focus between controls within the cells, you'll have to double-tab to move to the next control.

For example, if I have a textbox in a cell and want to move to a textbox in another cell within the datagrid with TAB, hitting TAB once will move me to the next DataGridCell... then I have to press TAB again to move to the TextBox inside that DataGridCell.

<span style="text-decoration: underline;"><strong>Solution</strong></span>

After googling around, I frequently hit this site which supposedly fixed this problem with a nice little solution: <a href="http://blog.yalovoi.net/2009/08/21/">http://blog.yalovoi.net/2009/08/21/</a>

For some reason unknown to me and not worth my time to investigate, it doesn't work at all. Here's what I came up with which is uglier but, in my case, works. I simply navigate the tree from the DataGrid to the textbox.

Forgive my quick and dirty coding but it gets the job done... I'm sure you could easily spawn a much more generic code to do this:

<pre name="code" class="c#">
        private void uxFieldMappingsDataGrid_CurrentCellChanged(object sender, EventArgs e)
        {
            uxFieldMappingsDataGrid.BeginEdit();
        }
        private void uxFieldMappingsDataGrid_PreparingCellForEdit(object sender, DataGridPreparingCellForEditEventArgs e)
        {
            ContentPresenter cp = (ContentPresenter)e.EditingElement;
            TextBox destinationTextBox = VisualTreeHelper.GetChild(cp, 0) as TextBox;
            if (destinationTextBox != null &amp;&amp; destinationTextBox.Name == "uxTest")
            {
                destinationTextBox.Focus();
            }
        }
</pre>

You can see where I climb the visual tree down to the text box. Very simple code for a very specific reason that I'm sure you can mold to make your own if you find that you are having the same problems as I am (and using code-behind to solve it isn't against your religion).