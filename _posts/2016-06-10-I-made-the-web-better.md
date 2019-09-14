---
title: I made the web better today, you can too.
layout: "post"
description: "Everyone, no matter how lame you think you are, can help make things better, for someone."
keywords: "foss, github, google, amp, accessibility, disability"
date: "2016-06-10 22:11:27 -0900"
---

A long while ago, say 5 years back, on the way home from a work trip from Bellevue, WA I purchased a book before getting on my flight. Thanks to the company's (now under a different name) liberal education policy regarding technical books, it was on them. 

The book I purchased, after some internet sleuthing on "good books for developers" or a similar keyword setup, was this guy:

<a href="https://www.amazon.com/gp/product/0321965515/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321965515&linkCode=as2&tag=papa00-20&linkId=d1e6c449884cd6257cb3f746d39a3f07" alt="Book: Don't make me think by Steve Krug">
	<amp-img src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=US&ASIN=0321965515&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL160_&tag=papa00-20"
		height="160" width="105" alt="Book: Don't make me think by Steve Krug" />
</a>

<!--excerpt-->

This book goes over good design, and it has been long enough that I can't recall other good bits about it (sorry Steve!). 
But on the flight from Bellevue back to D.C. I devoured this book. For a technical-ish book, this was the fastest read for me to this day.
One section in the book stands out immensely and had from that point on, always stood out for me, which was "Accessibility and you" (3rd edition, 2nd edition it was "Accessibility, Cascading Style Sheets, and You") where the author details
various practices or attributes to use to help make web pages you're working on accessible to those with some kind of disability. 

To quasi-quote from a 5 year old memory bank, "Accessibility is not the law now, but it will be" was another line that stuck out, because it is true. If you know a tornado of work is coming, why wouldn't you get ahead of it?

To brag a bit here, I went to Google I/O this year, on my own dime, thanks company? and went to a session on accessibility. 
Some of the statistics were amazing, 1 in 5 folks (US based) using the internet have some type of disability, for those that like statistics, thats 20% yall.
I reckon that if you work for a company, some subset of your user base has a disability and would love the option of navigating your elephant ear recipe site using a screen reader, or without squinting.

So, reigning in this mind dump of typing. How, Pat, did you make the internet better?

At Google I/O one thing kept popping up that the company is pushing, is Accelerated Mobile Pages, AMP for short, which is a technology that enforces really strict web design guidelines and adds in a few custom HTML elements, that the underlying code optimized for delivery.
For those with Android based phones, if you visit your News and Weather application, those little lightning bolts with AMP next to them indicates web pages that are using AMP. In fact, newer pages on this blog are using it, it is fast.

One of my more recent posts, [I just paid 70 for pjs](/2016/03/01/i-just-paid-70-for-pjs.html) , has an Instagram image, which AMP requires a special element for, `<amp-instagram>`. 
I got on a accessibility kick one night, trying to make this very site more if not most accessible using <a href="http://khan.github.io/tota11y/" target="_blank">tota11y</a>.
The constant error coming up, `img` tag does not have an `alt` attribute. Easy peasy right? Just add an `alt` attribute on the `<amp-instagram>` element and we move on.

Nope. Damn.
AMP validation kicks off that the alt tag is not allowed. 
(Non-Pro but documented tip: For an AMP enabled page add #development=1 on the URL, and view the console for errors)

Oh damn.

Enter <a href="https://github.com/ampproject/amphtml/pull/3520" target="_blank">PR of the century*</a> 
Open source allows you to fix stuff, and possibly get it in the final project, no matter how big or small the project is. I did say this was one of Google's flagship products right? Like incredibly pushed at Google I/O?
<i>*for me at least</i>

So I was able to identify a missing problem, that affected up to 20% of US internet users, with one of the largest tech companies in the world. Hows that feel?

<amp-img src="/assets/img/2016/06/10/feelsgoodman.jpg" alt="Feels good man frog meme" height="267" width="200"></amp-img>
Indeed...







