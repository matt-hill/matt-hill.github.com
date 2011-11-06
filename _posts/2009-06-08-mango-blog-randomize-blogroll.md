---
layout: default
title: Randomizing Your Blogroll in Mango Blog
tags: [ railo, coldfusion, mangoblog]
permalink: /post.cfm/randomizing-your-blogroll-in-mango-blog
---

My "Friendly Linkage" list to the right always displays alphabetically sorted, and while I do have a natural affinity for order and organization, I would like to mix it up a bit instead of always showing everyone I share links to listed in the same order (I know I know its the egalitarian in me really). I was going to make a Mango Blog custom tag to randomize your links for you, but then I came across this post by [Ben Nadel] which was really a follow up based on a comment by [Mark Mendel] in a previous post, and I then had to ask myself, "Does one line of code justify a whole custom tag?" Right now I'm going to go with "No". So here it is Mango users, if you want to randomize the links in your favorites list, edit the file: [siteroot]/tags/mangoextras/Links.cfm at line 30 from:

	<cfset favoriteLinks = event.getOutputData() />

to:

	<cfset favoriteLinks = event.getOutputData() />
	<cfset CreateObject("java","java.util.Collections").Shuffle(favoriteLinks) />

and bada bing bada boom, randomly sorted linkage. See that's even more friendly than before. Caveat: This does of course sort all list links everywhere you display them so that may not work for you. CFML engine note: This site runs on Railo btw so consider this tested on that engine, and I see no reason why it wouldn't work on Adobe CF, although it does use the CreateObject() method which some hosting services disallow so your mileage may vary.

[Ben Nadel]: http://www.bennadel.com/blog/280-Randomly-Sort-A-ColdFusion-Array-Updated-Thanks-Mark-Mandel.htm
[Mark Mendel]: http://www.compoundtheory.com/