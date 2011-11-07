---
layout: default
title: Time For A Change
tags: [ github, jekyll, liquid, markdown, textmate, bootstrap ]
---

Poor developer blogs. Every time their author finds a new engine, language, or inspiration, they're the first thing to get retooled or rewritten. And this blog is no exception. For the last few years, this blog has been running under [Mango Blog] on [Railo] hosted by the excellent hosting service [Alurium]. However, things change and I've recently stumbled onto the neat idea of hosting a blog through GitHub Pages. 

[GitHub Pages] is a free web publishing service for developers to host project documentation and other static documents just by pushing content to a GitHub repo. Leveraging this generous service and a few of its integrated features, one can produce a pretty functional blog that is very lightweight ( hard to get lighter ) and jives well with common developer toolsets and workflows. It seemed pretty appealing so I gave it a shot, and thought it would be fun and possibly helpful for others to walk through my approach to this project.

The key element to making use of the service as a blog 'engine' instead of just hosting static pages is a gem called [Jekyll]. A "simple, blog aware static site generator" as described by its author Tom Preston-Werner, Jekyll is built into the GitHub Pages publishing service, and with a sort of post-commit hook basically takes your repo and transforms it into a blog, but as HTML pages instead of say CFML, PHP, or the like.

So, how does this work? There's a few components involved. First off is the [_config.yml] file. This file resides in the root of your repo and helps Jekyll know how to parse and render your pages. It also serves as a config variable store which can be used to make decisions in your pages or populate data in your views. Mine can be seen [here].

Next up is [Liquid]. Liquid is a template rendering library written in Ruby for merging views with data, in this case populating your HTML pages with the content of your posts. Part of Jekyll's magic is Liquid. To pull an example from my own templates, it looks like this ( note the double curly braces which output the variables they wrap ):

	{% raw %}<h2><a href="{{ post.url }}">{{ post.title }}</a></h2>{% endraw %}

The general idea is that you build the HTML and CSS of your site to be used as includes or layouts, then use Liquid as the dynamic 'server side' aspect denoting where decisions are made and variables are printed within those includes and layouts. As you commit to your repo, Jekyll will melt the two together like a grilled ham and cheese.

This seems a good time to mention that I don't care for WYSIWYGs. They have their uses but among other oddities, I'm not fond of using them to transcribe code which I expect to appear a certain way. It typically doesn't. So a big part of the appeal for me in making this shift is that it will provide me with a much cleaner flow for blogging. In fact, it will conveniently be the same exact workflow as it is to develop ( at least in this ecosystem ). In most situations I'm an editor guy over an IDE guy and for some time now I have preferred TextMate. I've also been looking for an excuse to use Markdown so this seemed like a great time. Jekyll also supports both Markdown and Textile out of the box. Put this all together and it means I can write all my blog posts in either Markdown or Textile ( this is a Markdown post ), and Jekyll will translate the post content for me into HTML when I commit ( plus update my other pages automatically as dictated by my design ). And if I feel like writing some of my posts in Textile and others in Markdown, Jekyll can mix and match without tripping over itself. For me personally, this is a great flow. Of course time will tell if it actually affects my volume of posts but that's a different story for a different post ( that may never get written ).

"But hey, what about comments?", you're saying aloud to your monitor ( I know it's scary, huh? ). Well that's good news for you and a mixed bag for me. The good news is [Disqus], a free SAAS commenting system which is fairly common but one that I'm using for the first time. Its beauty, aside from the offering itself, is that it can be loaded into a page with a few lines of JavaScript, effectively turning your static HTML page into an evolving conversation. Once you create an account, there are a variety of code snippets in the dashboard to meet the needs of your site - Top Commenters, Recent Comments ( which I use on the front page ), etc. The mixed bag part for me is that as part of this move I'll be losing my existing blog comment history, which doesn't appear to be portable to Disqus from my outdated version of Mango Blog. I would say, "C'est la vie", but I don't know how to spell that, so I'll just say, "That's life". That's life.

The last element worth mentioning in this process is the redesign. Though I like the existing look, I wanted to go a different direction this time around; something a bit more fresh and clean. Having borrowed a bit from the very well done [Bootstrap] toolkit on a previous project, I thought I'd give it a stronger test run and see how much I could lean on it. And lean on it I did. There's currently only [40 lines of CSS] on this site that didn't come stock with Bootstrap. If you're not already familiar with this product, its worth looking at. Released by Twitter, its basically a ready-to-go CSS file that's got more than your basic elements already handled: forms, tables, headers, inputs, typography. There are even accompanying JavaScript files for providing basic modals, alerts, and the like. Hitting the ground running with Bootstrap for your design is as easy as checking out these two links ( in fact, its even easier if you just start with a pre-baked layout like I did ):

- [http://twitter.github.com/bootstrap/](http://twitter.github.com/bootstrap/)
- [https://github.com/twitter/bootstrap/blob/master/bootstrap.css](https://github.com/twitter/bootstrap/blob/master/bootstrap.css)

So in short, I've just vastly changed my workflow for blogging and I'm looking forward to seeing how it works out. I've also attempted to make my blog repo very [fork-friendly] by abstracting my own site-specific settings out of the layouts and includes and into the _config.yml. Delete the posts, change the hero unit include, and clear out the custom CSS, and you'll have yourself an instant blog. Enjoy.


[Mango Blog]: http://mangoblog.org
[Railo]: http://getrailo.org
[Alurium]: http://www.alurium.com
[GitHub Pages]: https://pages.github.com
[Liquid]: http://liquidmarkup.org/
[Jekyll]: https://github.com/mojombo/jekyll
[_config.yml]: https://github.com/mojombo/jekyll/wiki/configuration
[here]: https://github.com/matt-hill/matt-hill.github.com/blob/master/_config.yml
[TextMate]: http://macromates.com/
[Disqus]: http://disqus.com/
[40 lines of CSS]: https://github.com/matt-hill/matt-hill.github.com/blob/master/css/custom.css
[Bootstrap]: http://twitter.github.com/bootstrap/
[fork-friendly]: https://github.com/matt-hill/matt-hill.github.com/