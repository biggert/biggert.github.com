---
layout: post
title: "Open source OCR Technologies (or lack thereof)"
description: ""
category: ""
tags: [OCR]
---
{% include JB/setup %}

So I could post about how I've completely ignored this blog for months... but that would take time to explain my new job and all that jazz. I'd rather post about how baffling it is that, as old as OCR tech is, there's just not any good open-source libraries available that are even comparable to commercial libraries. Now I understand that comparing open-source projects (or just closed-source freeware) to commercial projects are sometimes light and day but in my experience, especially over the past 5 or so years, it's almost like MOST open-source or freeware projects are at least a great subset of the commercial versions... if not better in some regards.

Let's start with what's out there that's the most popular mentioned OCR library available, <a href="http://code.google.com/p/tesseract-ocr/">Tesseract</a>. I see on the Google project site that this was one of the top 3 OCR engines in 1995. I feel sorry for people in 1995. I've got experience with commercial OCR engines like <a href="http://www.leadtools.com/sdk/ocr/default.htm">LeadTools</a> and even the simple one like <a href="http://msdn.microsoft.com/en-us/library/aa167607(v=office.11).aspx">Microsoft Office Document Imaging (MODI)</a> and they're much better than Tesseract.

Then there's <a href="http://www.simpleocr.com/">SimpleOCR</a>. They're closed source but freeware. Thanks to those guys for providing a freeware and royalty-free SDK but man, it's absolutely terrible. In their defense, I don't think it is maintained anymore (it doesn't even support color) but could take a screenshot of the letter S and this library would tell me it's a T. Bleh. I've heard MODI is powered by the same engine as SimpleOCR but if that's true, you'd expect similar results which you don't get.

Now here's one I want to try - <a href="http://research.microsoft.com/en-us/um/redmond/projects/hawaii/students/default.aspx">Microsoft Research Project Hawaii, OCR in the Cloud</a>. I don't know how fully featured or how dependable this is since it's a research project but as soon as I get some free time, I'm gonna try it out. I've tried <a href="http://www.wisetrend.com/wisetrend_ocr_cloud.shtml">WiseTREND's OCR Cloud</a> service and I love it... it's fast and super accurate (uses their ABBYY engine) and also supports a lot of file types... but if I want to distribute an opensource desktop application that doesn't a) require internet connectivity and b) more importantly doesn't require per document pricing, WiseTREND is obviously not an option.

Just a rant on OCR products... maybe I'm wrong about some of things I said and maybe there are better alternatives out there.... which hopefully both are true and some commenters will lead me on a better path. Overall, OCR in the Cloud is great because of how expensive OCRing (and ICR even more so) is on any processing machine so it'd be great to see more options of this nature but my only problem from the litigation world is that I don't think lawyers are exactly comfortable sending privileged client data over web for this so in a lot of cases, desktop-only solutions are the only solution.