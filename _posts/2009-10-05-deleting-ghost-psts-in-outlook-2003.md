---
layout: post
title: "Deleting Ghost PSTs in Outlook 2003"
description: ""
category: ""
tags: [Outlook]
---
{% include JB/setup %}

Had to give a shout out to <a href="http://www.outlook-tips.net">www.outlooktips.com</a> for helping me with my latest problem. Due to some testing of some code based around the third-party library named <a href="http://www.dimastr.com/redemption/">Outlook Redemption</a>, I had a few "ghost" PST folders left around in Outlook. I've had this in the past and the best solution out there was to literally remove the mail profile and add a new one. Because my current profile consists of an incredibly large exchange account (I've taken the Gmail approach where I archive messages instead of deleting) and I did not want to redownload all those darned emails... so I found this link: <a href="http://www.outlook-tips.net/howto/ghosts.htm">Delete Ghost PSTs by Editing the Registry</a>. Crisis averted! One note that I wanted to add though is that this tells of searching for 001e3001 in the registry to find the name... my names were actually stored in 001f3001. Luckily the name in my particular case was easily identifiable so once I deleted the key, the folder was gone.