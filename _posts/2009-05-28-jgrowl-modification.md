---
layout: default
title: jGrowl Modification
tags: [ javascript, jquery, jgrowl ]
permalink: /post.cfm/jgrowl-modification
---

If you haven't yet checked out [jGrowl], you should. Its a jQuery plug-in that emulates a notification system on OS X known as [Growl]. It provides a fixed position popup in the corner of the web page and can be used to alert your visitors to any sort of information you choose. Multiple "growls" stack very cleanly beneath each other and can either "stick" to the page or fade away at a configurable interval. It's really pretty slick.

Anyway, I recently had a need to programmatically remove individual sticky popups from the page while leaving the others in place. With the current release of jGrowl, I couldn't find a good way to do this. You can set the messages to fade on their own, or let the user click the close button on stickies, or programmatically close them all, but I could not find a way to just remove a specific popup without affecting the rest of them, so I added a few lines of code to the jquery.jgrowl.js file which allows me to pass an id as an additional option that gets assigned to the individual message being created. I can then later target and remove that specific popup with more jQuery/jGrowl magic (or check to see if it already exists and save potential notification duplication in the case of an ajax polling situation or the like). Instead of uploading and linking to the changed file here which would grow stale over time if jGrowl is rereleased, I'll just list the lines I changed for others to implement in their own copy (for clarity, these are the lines as they exist in the uncompressed version).
change lines 117-118 from:

	theme: 'default', corners: '10px',

to:

	theme: 'default', growlId: '', corners: '10px',

and line 162 from:

	var notification = $('
		"close">' + o.closeTemplate + '
		"header">' + o.header + '
		"message">' + message + '
	')
 
to:

	var notification = $('
		"close">' + o.closeTemplate + '
		"header">' + o.header + '
		"message">' + message + '
	')
 
To add an id to the specific growl, just add it as an additional option like this:

	$.jGrowl(message, { closer: false, growlId: 'thisGrowlId', theme: 'default', sticky: 'false' } );

And use this to target and remove that specific growl:

	$("div#" + growlId).trigger("jGrowl.close").remove();

Why would you want to do this? Perhaps for form validation and the messages are removed when you meet the validation rules, or maybe you want to keep all your messages as stickies and you have an ajax method polling their current relevancy related to some system issue (like keeping a notification up that some service is unavailable, then removing that message when it comes back online without removing any others that might be on the screen), or any of several other completely random reasons, but if you ever do find a need for this functionality, here you go.

[jGrowl]: http://www.stanlemon.net/projects/jgrowl.html
[Growl]: http://growl.info/