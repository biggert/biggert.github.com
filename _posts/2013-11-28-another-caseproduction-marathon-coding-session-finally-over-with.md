---
layout: post
title: "Another CaseProduction marathon coding session finally over with..."
description: ""
category: ""
tags: [C#]
---
{% include JB/setup %}

I'm sure there are plenty more ahead but I just spent 4 days rewriting a big piece of our code to support serialization and boy was it a doosey. By doing this, we can easily save our class (and all its children collection properties) straight to a file (XML) and load straight from the file using System.Xml.Serialization.XmlSerializer. From the user's perspective, this allows them to save CaseProduction jobs to a file and load from a file with ease. Using XmlSerializer is probably nothing new to anyone else as it's been around since .NET 2.0 but it was fun to work with, especially since I'm used to manually reading/writing XML files in our WayPoint product. The only problem I had was actually with how the classes were originally built using an underlying DataSet. I could've either taken two paths: write hack after hack to each class to iterate through all the properties and correctly link up to the underlying DataSet or just go through and remove the underlying DataSet completely. I took the later approach and the result is great... a nice lean class using .NET collections without any of the hassle of DataSets.

I doubt there's anything new here to share but one thing I did notice that took some time to figure out didn't work and had to go back to rewrite some of it... in my move away from using an underlying DataSet, I changed our properties to the new C# 3.0 automatic getter/setter properties. This are fun and make coding a lot quicker and I actually prefer the setting of default values for this properties in constructors or initialize methods instead of having a separate, private variable declared but I my Googling brought me to using the System.ComponentModel.DefaultValue() attribute. There are a couple of blog/forum posts out there that led me to believe using this attribute will set the default value of an automatic property. This is not true at all.... this attribute is only used in the visual designer. A stupid mistake that I made and required a lot of trial and error to figure out "Oh crap, that doesn't work at all". Just wanted to give it a special mention so this doesn't happen to anyone else.

Now off to saving the contents of a WPF Toolkit Datagrid to a file...