---
layout: post
title: "Installshield edit field browse button restricted to UNC paths via WiX"
description: ""
category: ""
tags: [Installshield]
---
{% include JB/setup %}

This took an incredible amount of research and, 2 years ago, I actually told my superiors it could not be done (based on our previous architecture, this was true). I wanted to make sure I shared it on the internet now that I finally solved what seemed to be such a simple thing to ask for from the installer.

We are using Installshield 2012 Spring and have a basic MSI project (Installshield version shouldn't matter). Also, we have incorporating the <a href="http://wix.codeplex.com/">WiX</a> into our architecture which allows us to use C# .NET custom actions which is honestly a Godsend for Microsoft .NET development firms IMO. While this post isn't intended to detail how to use these types of custom actions, I do touch on it a little for those who want to know. Also, I reference the customized Windows Folder Browser dialog too... again, this post isn't intended to show how to write this (and customize it) but I do get into that a little for those who again are eager to know.

First off is our Installshield project setup... we've got a blank dialog in the installer that has an edit field and a button - this provides the basis for every "enter the path" dialog you've probably seen in the app world. The edit field is tied to a property, let's call it "PATH", and the Browse button has events associated with it, one that simply sets '\[PATH\]' to '\[PATH\]' and then the more important one that calls a DoAction on a .NET WiX Custom action that actually shows the folder browser dialog.

<img class="alignnone" alt="" src="http://i.imgur.com/gE9ACCl.png" width="475" height="214" />

&nbsp;

The WiX custom action in C# looks like so:

<img class="alignnone" alt="" src="http://i.imgur.com/W6feStt.png" width="567" height="326" />

<img class="alignnone" alt="" src="http://i.imgur.com/VqUStkZ.png" width="538" height="167" />

This one simply hands off to a more generic function that shows a customized version of the FolderBrowser dialog in Windows. Without getting too much into it, this dialog comes from the Win32 API and is exactly what we want/need as far as customization... in our case, we limit it to the 'network neighborhood' (only network paths). You can read more about it <a href="http://support.microsoft.com/kb/306285">here</a>.

Moving on, this dialog saves the results of the selected path to our \[PATH\] property (via WiX) and we can see that change in our Installshield dialog. Now, one of tough parts was getting all the .NET code situation to limit our selection to UNC paths... the user can certainly provide a custom local path but we guard around that as much as we can. The hardest part was this... clicking the Browse button in Installshield immediately fires the 2 events associated with it... and worse, the UI feedback loop doesn't wait for the Custom action to respond - so when the custom action fires to show the Folder Browser dialog, the Installshield UI is done... meaning that the user selects the path and the folder browser dialog closes and we have the assignment of the value to our \[PATH\] property but the edit control doesn't get updated!

Here's where the baffling part of Installshield/MSI comes into play... you must go edit the ControlEvent table to allow this to happen in a synchronous manner so that the Edit control <em>does</em> get updated properly <strong>AFTER</strong> the folder browser dialog closes. Specifically, open the Direct Editor in Installshield, select the ControlEvent table and find the entries for the Dialog box and the button, put a 0 for the DoAction Event in the Ordering column and a 1 in the property event in the ordering column.

<img class="alignnone" alt="" src="http://i.imgur.com/s3RQBMX.png" width="906" height="43" />

&nbsp;

So now you should have a normal working dialog where the user can either specify the path by typing it in or clicking the browse button to specify it using the folder browser dialog. As simple as that sounds, it requires way too much backend manipulation to get it working smoothly.

<strong>NOTE: It appears that if you make changes to the dialog or possibly even view it in the designer in Installshield, it will overwrite the Ordering column in the ControlEvent table so make sure you don't revert these settings when you save!</strong>

&nbsp;