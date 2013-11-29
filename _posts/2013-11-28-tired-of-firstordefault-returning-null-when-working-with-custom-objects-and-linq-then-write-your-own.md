---
layout: post
title: "Tired of FirstOrDefault returning NULL when working with custom objects and LINQ? Then write your own"
description: ""
category: ""
tags: [c#]
---
{% include JB/setup %}

So I finally got to work with LINQ in our current .NET 3.5 project as I haven't had a chance to use it yet in business projects, just personal projects which usually resulted from curiosity. I know, I know, it's newness has worn off since it's been around since .NET 3.0 but hey, whattyagonnado? Anywho, I began working with LINQ centered around some custom classes and collections we had written.

As I being working with this, I specifically came across a few use-case scenarios for FirstOrDefault(). I could use this function with a conditional clause and knock out a lot of clunk codeblocks that I used in different parts of the application. Then I quickly found the pitfall of using this with my custom object... it returned NULL if not found. This required me to write 2 more lines of code to checks for NULLs which I felt was a bit wasteful so I was steered by Google to <a href="http://blog.dynamicprogrammer.com/2009/05/28/FirstOrNullObjectExtensionMethodForIEnumerableAndFirstOrNew.aspx">http://blog.dynamicprogrammer.com/2009/05/28/FirstOrNullObjectExtensionMethodForIEnumerableAndFirstOrNew.aspx</a> which taught me to write my own FirstOrDefault type of function which allows me to define the default value that is returned if a value is not found. If you want actual information about it, please read his post above. I'm just providing the code I wrote as a result of reading his excellent post.

Here is my LINQHelper class I came up with. These extension methods give me the ability to prevent the returning of a NULL object with my custom classes which reduces the amount of code I have to write in the long run. I also went ahead and extended the LastOrDefault methods as well.
<pre name="code" class="csharp">
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace BusinessLogic
{
    public static class LINQHelper
    {
        public static T FirstOrNullObject&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T nullObject)
        {
            var val = enumerable.FirstOrDefault&lt;T&gt;(func);
            if (val == null)
            {
                val = nullObject;
            }
            return val;
        }
        public static T FirstOrNullObject&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T nullObject)
        {
            var val = enumerable.FirstOrDefault&lt;T&gt;();
            if (val == null)
            {
                val = nullObject;
            }
            return val;
        }
        public static T FirstOrNew&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T newObject)
        {
            return enumerable.FirstOrNullObject&lt;T&gt;(func, newObject);
        }
        public static T FirstOrNew&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T newObject)
        {
            return enumerable.FirstOrNullObject&lt;T&gt;(newObject);
        }
        public static T FirstOrDefault&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T defaultObject)
        {
            return enumerable.FirstOrNullObject&lt;T&gt;(func, defaultObject);
        }
        public static T FirstOrDefault&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T defaultObject)
        {
            return enumerable.FirstOrNullObject&lt;T&gt;(defaultObject);
        }
        public static T LastOrNullObject&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T nullObject)
        {
            var val = enumerable.LastOrDefault&lt;T&gt;(func);
            if (val == null)
            {
                val = nullObject;
            }
            return val;
        }
        public static T LastOrNullObject&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T nullObject)
        {
            var val = enumerable.LastOrDefault&lt;T&gt;();
            if (val == null)
            {
                val = nullObject;
            }
            return val;
        }
        public static T LastOrNew&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T newObject)
        {
            return enumerable.LastOrNullObject&lt;T&gt;(func, newObject);
        }
        public static T LastOrNew&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T newObject)
        {
            return enumerable.LastOrNullObject&lt;T&gt;(newObject);
        }
        public static T LastOrDefault&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, Func&lt;T, bool&gt; func, T defaultObject)
        {
            return enumerable.LastOrNullObject&lt;T&gt;(func, defaultObject);
        }
        public static T LastOrDefault&lt;T&gt;(this IEnumerable&lt;T&gt; enumerable, T defaultObject)
        {
            return enumerable.LastOrNullObject&lt;T&gt;(defaultObject);
        }
    }
}
</pre>
Once again, this information was gathered from Mr. Garcia's blog at <a href="http://blog.dynamicprogrammer.com">http://blog.dynamicprogrammer.com</a>. I give him full credit for this information laid out in a very explanatory blog post.