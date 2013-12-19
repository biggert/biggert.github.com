---
layout: post
title: "Virtualized WPF Listbox scrolling (because ScrollIntoView doesn't always work)"
description: ""
category: ""
tags: [C#,WPF]
---
{% include JB/setup %}

<p>
I guess I'll start this off the fun way... with a recent issue I was involved with yesterday regarding a rogue list box. So to explain the issue, I've got a virtualized list box full of nice little custom objects. The user has access to delete these items from said listbox. The problem comes into play where, if the user has scrolled down the listbox but then deletes the items they are looking at and the scroll bar disappears (it will disappear if the number of items in the listbox is less than the amount that needs a scrollbar), the user can no longer scroll to the top of the listbox. So the items will be inaccessible!
</p>
After spending a little time Googling and realizing that ListBox's ScrollIntoView did nothing, I found an excellent forum post that detailed the notion of directly accessing the scrollviewer inside the listbox Once I had access to that, I could scroll all I wanted to.

I basically just added this function:
```csharp
private childItem FindVisualChild<childItem>(DependencyObject obj) where childItem : DependencyObject
        {
            for (int i = 0; i &lt; VisualTreeHelper.GetChildrenCount(obj); i++)
            {
                DependencyObject child = VisualTreeHelper.GetChild(obj, i);
                if (child != null &amp;&amp; child is childItem)
                {
                    return (childItem)child;
                }
                else
                {
                    childItem childOfChild = FindVisualChild&lt;childItem&gt;(child);
                    if (childOfChild != null)
                    {
                        return childOfChild;
                    }
                }
            }
            return null;
        }
```        
Adding a call to it to walk the visual tree for the scrollviewer:
```csharp
ScrollViewer sv = FindVisualChild&lt;ScrollViewer&gt;(uxListBox);
```
And that's it! Now I can sv.ScrollToTop(), ScrollToBottom(), or even specific vertical/horizontal offsets. I do have to make a call to ListBox.UpdateLayout() to refresh but it's all good now... crisis #93487 averted!

Thanks to <a href="http://channel9.msdn.com/forums/TechOff/261274-Accessing-WPF-Control-parts-from-code/" target="_blank">this post</a> for guiding me to the light!
