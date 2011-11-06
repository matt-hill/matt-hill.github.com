---
layout: default
title: "ColdFusion Wish: var=true Attribute"
tags: [ coldfusion, railo ]
permalink: /post.cfm/coldfusion-wish-var-true-attribute
---

I like CFCs. I enjoy building and using them. I like encapsulating my business logic within them, and extending and reusing them wherever I can. They are typically the brains in any project I architect. However, one thing has always bothered me about their implementation: the fact that any variable I create is not contained by default within that method, but rather you have to explicitly var a variable in order to keep it inside the method. To me, this is completely backwards. IMHO, it should be the other way around. It should be that every variable you create inside a method is by default contained within that method. That would be ideal. Someone may mention the upcoming local scope in CF9, and I look forward to that easing the annoyance, but as I understand its proposed implementation it doesn't actually solve the problem. It just makes it less prominent for the developer. Its a bandaid for the components' intrinsic propensity to bleed data.

I realize that the current behavior is extremely unlikely to change in the near future, and even if I could snap my fingers and make it change, I probably wouldn't because doing so would break a lot of code everywhere, including my own. But in the imaginary world where my opinion has an affect on the CFML landscape at large (Adobe/Railo/OpenBD), how about this for a compromise:

	<cffunction name="doSomething" access="public" output="false" var="true" returntype="boolean"></cffunction>

or even:

	<cfcomponent output="false" var="true"></cfcomponent>

Did you notice the var="true"? How great would it be if all you had to do was add this attribute to your method or even just to your cfcomponent tag, and it would define a behavior within the component that by default contained all unscoped variables within the methods in which they were created? And further, perhaps the only way to push them out of the method was to stick them into another scope like the component's variable scope? To me, this would be a supremely beautiful thing. If such a thing existed, this behavior would also ignore any existing var references within the affected method or component (and not throw any errors) since they would all effectively be varred anyway. That way it would be backward compatible for older code. Then we could all navigate to our CFCs, throw that little attribute at the top, and boom, no more data bleeding because you reused the same list index and forgot to var it in one of your methods. No more having to run other applications just to parse your code and tell you where you forgot to explicitly declare what should be an internal variable anyway.
Perhaps I'm on my own with this sentiment, but I just felt like soapboxing to the interwebs about this. Thanks for reading.