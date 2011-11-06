---
layout: default
title: Fun With Reserved Words In ColdFusion
tags: [ coldfusion ]
permalink: /post.cfm/fun-with-reserved-words-in-coldfusion-1
---

So I was randomly curious about ColdFusion's implementation of reserved words, specifically true and false. I wondered, "Can true be set to false in ColdFusion?" You may ask "Why would you ever want to do this?" I might respond "No frakking idea." But here is my attempt all the same.

	<cfset true = false />

throws the error "invalid construct", as does:

	<cfset true = "false" />

I can do this:

	<cfset "true" = false />

but it just puts a new key in the variables scope (variables.true) which is trumped in business logic by the real true, so not much point.

So the answer to the question near as I can tell is: No, you cannot set true to false in ColdFusion. If anyone has any tricks I didn't think of, feel free to comment as I'm sure they could be no more frivolous than this post itself.