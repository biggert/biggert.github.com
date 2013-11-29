---
layout: post
title: "Installshield Major Upgrade not migrating feature states"
description: ""
category: ""
tags: [Installshield]
---
{% include JB/setup %}

Just a quick blurb - I just spent the last week trying to find out why the hell my installer didn't properly migrate the feature states during a major upgrade. Upon researching this at length on the Flexera forums, I finally found it out myself. I had a dialog set the InstallLevel to certain value depending on the type of license key that was entered. It appears that, during upgrades, changing the InstallLevel via the SetInstallLevel action on a button will cause your features to revert to a full install.

So, in my case, if you installed selecting only 2 of 4 features and then did an upgrade on that install, you'd get all 4 features installed after upgrade. Once I modified the condition of this action to not set the InstallLevel during upgrades, post-upgrade, you only get the 2 features you originally installed with.

Just wanted to get this info out there since it wasn't easy to figure out...