---
layout: post
title: "Quick way to lower CPU usage in heavy WPF animation desktop app"
description: ""
category: ""
tags: [C#,WPF]
---
{% include JB/setup %}

Earlier this week, we ran into an issue where our desktop application (WPF heavy) was attacking our CPU cycles. Upon further investigation, all problems pointed to our lovely progress spinning controls which are powered by looping WPF animations. After some dabbling with replacing the animations with animated GIFs turned out to be more than its worth (and still gobbled a few cycles), we decided to go with a lovely suggestion from the <a href="http://social.msdn.microsoft.com/Forums/en-US/wpf/thread/ba95b75f-6cfd-478e-af7a-9954dee8a1b9">MSDN forums</a> about reducing the frames per second on the WPF animations update.

The result was this simple little piece of code:
```csharp
Timeline.DesiredFrameRateProperty.OverrideMetadata(typeof(Timeline), new FrameworkPropertyMetadata { DefaultValue = 20 });
```

A small reduction in the visual refresh rate down to 20 FPS (not easily noticeable to the user) resulted in a huge decrease in CPU usage... from over an average of 30% CPU usage down to an average of 5%.

On a separate note... word to the wise, don't bind properties directly to UI elements in WPF which internally make database calls... even if you load the items asynchronously, WPF will bind and make the DB calls on the main thread which will block the UI.

