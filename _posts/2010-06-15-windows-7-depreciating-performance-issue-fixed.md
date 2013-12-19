---
layout: post
title: "Windows 7 depreciating performance issue fixed"
description: ""
category: ""
tags: [Windows]
---
{% include JB/setup %}

I know this is probably more worthy of a tweet but considering the amount of time I've spent with this, I though I'd get it out there on the blogosphere for archival and searching purposes.

At Microsoft's PDC2009 last year, they put out some pretty sweet Windows 7 Ultimate laptops. For the last 6 months, I began to actually use it pretty heavily for development and other things. I noticed over time whether the laptop was simply sitting on the desk for a long period of time (open or closed), in standby mode, or even just hibernation, the performance would decrease over time. The RAM usage would be high but the CPU and all that was fine. After running a few process monitoring applications as well as RAM defraggers, I had no success in bringing the machine back to it's "cold-boot" state. Even odder, I would notice that, when an application was running, when I initially would click on it in the taskbar to bring it up, it would literally take minutes to come back but oddly enough, as I used it, it became faster and faster as if it was caching itself again. So even though the laptop itself upon new application and the basic OS environment would be slow, applications themselves would catch back up to speed eventually (the Add Reference dialog in VS2010 was still atrociously slow though every time it opened :)). The best thing was always to save whatever I was doing and then restart everytime... so basically I'd sit down, open the laptop and, if I was doing anything more than email checking, restart... this was faster than waiting for the application to catch up.

After extensive Googling, I never really found a solid solution... some people had similar situations but the one's that had solutions were either getting rid of a windows service, changing out hardware, or reinstalling the OS. I gave up for a little while and just dealt with it... but recently installed Windows 7 on my desktop machine. I noticed real quick that my desktop machine could run for days and <strong>never</strong> experience this problem so I sat the laptop down side-by-side and called upon the computer gods to figure it out.

On the laptop, since it was my first venture into Win7, I added a few gadgets to the sidebar: CPU monitor, calendar, and clock. On my desktop Win7 machine, I just didn't get around to using the sidebar. Although it took me a while to notice this, I decided this was enough to investigate as a difference. Lo and behold, I removed the sidebar from the PDC Win7 laptop and it is now just as speedy on the fifth day of using it as it was in the first 10 minutes.

So, just to clearly put it, <strong>turn off the sidebar in Windows 7 for optimal performance</strong>. Don't know if anyone out there can apply this solution to the same problem with success but it doesn't hurt.

You can turn off the sidebar by using the following instructions:

1. Open the control panel and click Programs and then Programs And Features. On the left panel, you'll see "Turn Windows features on or off".
<p style="text-align: left; padding-left: 60px;">﻿<a href="http://i.imgur.com/PNpMWgw.png"><img class="alignnone size-medium wp-image-258" title="windows71" src="http://i.imgur.com/PNpMWgw.png" alt="" width="300" height="90" /></a></p>
<p style="text-align: left;">2. Click the button/link and uncheck 'Windows Gadget Platform'</p>
<p style="text-align: left; padding-left: 60px;"><a href="http://i.imgur.com/cBhyhkf.png"><img class="alignnone size-medium wp-image-259" title="windows72" src="http://i.imgur.com/cBhyhkf.png" alt="" width="300" height="262" /></a></p>
<p style="text-align: left;">3. Click OK and you're finished.</p>
<p style="text-align: left;"></p>
<p style="text-align: left;">The only bad thing is you don't get to use the sidebar :)</p>
<p style="text-align: left;"></p>
<p style="text-align: left;">NOTE: I'm not sure if turning off the sidebar or just getting rid of the gadgets I was using (CPU monitor, Calendar, Clock) make a difference so maybe if you need the sidebar, you could simply remove these gadgets and see which one is the problem.</p>
<p style="text-align: left;"></p>
<p style="text-align: left;">UPDATE (07/13/2010): Looks like the sidebar has nothing to do with this... looks to be an <a href="http://www.brianpeek.com/blog/archive/2010/01/31/acer-1420p-leaky-handle-driver-fix.aspx" target="_blank">Acer driver problem</a>.</p>
