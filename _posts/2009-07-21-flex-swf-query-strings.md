---
layout: default
title: "Flex, SWFs, And Query Strings"
tags: [ flex, coldfusion ]
permalink: /post.cfm/flex-swfs-and-query-strings
---

I'm very new to Flex so this small post is as much to note my findings as it is for anyone else that may come across it and benefit (I have a memory like the guy from Memento). Anyway, today I encountered difficulty getting my SWF to read the query string. If I called the SWF directly, passing the query string to it like so:

	http://mysite/myflexapp.swf?thisparam=1&thatparam=true

then it worked fine, but if I loaded the SWF from a wrapper page either via <object/> tag OR the commonly used AC_FL_RunContent() method, no luck. In the end, it was because the SWF can't read the query string passed to the wrapper page even though its, if you will, contained within that page. You must pass your variables along with the call you make via either method mentioned above in order for the SWF to see them, so with an <object/> call, just add this extra parameter and you're good:

	<param name="FlashVars" value="#cgi.query_string#">

With the AC_FL_RunContent() method, when you declare the src attribute, just add the query string to the end of the attribute's value, but make sure to leave off the .swf. Like so:

	AC_FL_RunContent(
            "src", "myflexapp?#cgi.query_string#",

Also, passing the whole query string to the calls means you don't have to edit these pages if you add or change URL parameters later. Hope this helps someone.