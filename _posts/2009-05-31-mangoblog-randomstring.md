---
layout: default
title: RandomString Plugin for Mango Blog
tags: [ coldfusion, mangoblog ]
permalink: /post.cfm/randomstring-plugin-for-mango-blog
---

Well, I've been running [Mango Blog] on [Railo] for about a week now, and I'm very satisfied with it overall. Mad kudos to Laura Arguello from [AsFusion]. Coming from a WordPress (PHP blog) environment, I'm particularly impressed with its plugin architecture. After doing some research a couple days ago (thanks [Adam Tuttle] for your tutorials), I spent a few hours today building my first plugin. While I'm very comfortable with CFCs and custom tags, I've never worked with an event-based/broadcasting architecture before. It was very different for me and quite compelling to figure out. (Its been a good few years since I printed source code to review away from the computer lol).

While I'm certain I've only scratched the surface with the Mango Blog engine, I believe I've managed to produce my first addition to the Mango Blog community with RandomString. This plugin allows you to output a different phrase, quote, magical incantation, or any other sequential string of words you choose, every time your page is refreshed. An example of its use can be seen at the top of this site underneath the logo (refresh to see the tagline change).

The list content for the plugin is managed through the Mango Blog admin settings page (once installed and activated), and can be configured to work as a pod (like in your sidebar), or can be called directly as a custom tag like this:

	<mangox:randomString />

The [RandomString plugin can be downloaded here]. I am also submitting the plugin to RIAForge.com and it would be my first submission to that site as well. I could not find a place to upload or submit the plugin to Mango Blog's site. Perhaps someone will point me in the right direction there. Anyway, I hope you all enjoy it. Thanks for the great work with Mango Blog! Also, of course, ColdFusion rules!

[Mango Blog]: http://www.mangoblog.org/
[Railo]: http://www.getrailo.org/
[AsFusion]: http://www.asfusion.com/
[Adam Tuttle]: http://fusiongrokker.com/archives/category/mango
[RandomString plugin can be downloaded here]: http://moonlitscript.com/assets/content/randomString.zip