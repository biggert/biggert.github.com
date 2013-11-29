---
layout: post
title: "Handling Secondary Thread Exceptions in WPF"
description: ""
category: ""
tags: [C#,WPF]
---
{% include JB/setup %}

As I'm sure you know, if you've played around in WPF enough, you've realized that the WPF way to catch unhandled exceptions is through the App.xaml with the DispatcherUnhandledException event. What you may not know is that this only catches unhandled exceptions in the WPF application itself. If you have any threads that throw exceptions or especially secondary threads (created by threads) that throw exceptions, you can kiss your pretty little "catch-all" event bye because your app with crash into the fiery pits of Windows system event log hell.

Recently on a project I've been involved with, we've been seeing this issue pop up a few times and without any knowledge from the event log, we really had a tough time finding the source of the errors. Enter the throwback to .NET 2.0, CurrentDomain's UnhandledException event. Our old little pal is back from the past to make an appearance in our pretty little WPF app and, lo and behold, we are able to catch those nasty unhandled exceptions in our secondary threads and perform a more graceful shut down. Very nice and very clean all with a simple code block:

<pre name="code" class="csharp">

private void Application_Startup(object sender, StartupEventArgs e)
{
AppDomain.CurrentDomain.UnhandledException += new UnhandledExceptionEventHandler(CurrentDomain_UnhandledException);
}

void CurrentDomain_UnhandledException(object sender, UnhandledExceptionEventArgs e)
{
//Oh noes! An error occurred!
}
</pre>

Now to actually fix the source of the errors!

NOTE: For added fun, if you fancy the use of legacyUnhandledExceptionPolicy, this gets event better.