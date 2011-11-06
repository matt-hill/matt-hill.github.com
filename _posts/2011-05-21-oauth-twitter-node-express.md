---
layout: default
title: How To Use OAuth and Twitter in your Node.js / ExpressJS App
tags: [ oauth, twitter, node.js, expressjs ]
permalink: /post.cfm/how-to-use-oauth-and-twitter-in-your-node-js-expressjs-app
---

So i'm pretty new (about a month in) to the beautiful creature that is [Node.js] and am playing with building an app where I'm not particularly interested in requiring its users to remember yet another set of login credentials as they surf on the intarwebs (nor am I interested in maintaining them), so it was a short jump to OAuth. If you're not familiar, OAuth basically allows your users to authenticate for your site using credentials from another site they frequent (Twitter, Facebook, Google, LinkedIn, etc). That system in turn provides you with unique identifier information about that user (like their username and user id) in order for you to store data against that user for your app or system without requiring, storing, or ever even seeing their password. Convenient. A quick scan on github produced [node-oauth], written by Ciaran Jessup, which appears to be a pretty well used wrapper module and is available on npm (its currently #17 on the 'depended on' list). So lets install that first.

	$ npm install oauth

That was easy. Next is the service we intend to work with. First up for me was Twitter (I may look at others later). In order to work with Twitter we need a few pieces of information from them for our OAuth code to work properly, namely: a Consumer Key, a Consumer Secret, and a few routing URLs. To get that information, register your application at [devtwitter]. Note that when you're filling out the form and you choose Browser over Client as your type of app, you'll need to enter a Callback URL. It doesn't matter what because we'll override it anyway in the code (you can just put your domain), but if you omit it, when you save the form, there appears to be a bug where it will revert to a client app which will then throw errors in your oauth calls downstream. Also noteworthy, I don't need write access to Twitter for this app, so I'm only asking for read-only. As a general rule of thumb I consider it a best practice to only ask of a user what you really need to make your app work and if you intend to write to their feed or on their wall, wherever possible at least give them options to enable or disable that functionality. Doing otherwise is kinda douchey. Anyway, once you register, it should route you to the details page wherein you should see the items of note mentioned above. Keep that page around for a bit, we'll come back to it.
So, as mentioned in the title, this is an app using the [ExpressJS] framework (which is awesome btw), so I'm leveraging its routing for my authentication and callback logic (to receive and use the user info coming back). We're also going to use the oauth module to hold the conversation with Twitter for us. So add this to the top of your app.js (or server.js if that's how you roll), and update the parameters with your info from the twitter dev page.

	var OAuth= require('oauth').OAuth;
	
	var oa = new OAuth(
		"https://api.twitter.com/oauth/request_token",
		"https://api.twitter.com/oauth/access_token",
		"YourConsumerKeyProvidedByTwitter",
		"YourConsumerSecretProvidedByTwitter",
		"1.0",
		"http://yourdomain/auth/twitter/callback",
		"HMAC-SHA1"
	);
	
Next, we'll add two routes to your app. This one does that call to Twitter wherein your user will be provided with your app's information as you registered it and be prompted to either continue with authentication and be routed back to your site, or cancel the authentication and make like a tree:

	app.get('/auth/twitter', function(req, res){
		oa.getOAuthRequestToken(function(error, oauth_token, oauth_token_secret, results){
			if (error) {
				console.log(error);
				res.send("yeah no. didn't work.")
			}
			else {
				req.session.oauth = {};
				req.session.oauth.token = oauth_token;
				console.log('oauth.token: ' + req.session.oauth.token);
				req.session.oauth.token_secret = oauth_token_secret;
				console.log('oauth.token_secret: ' + req.session.oauth.token_secret);
				res.redirect('https://twitter.com/oauth/authenticate?oauth_token='+oauth_token)
		}
		});
	});

This is the path that Twitter will route your user back to once they authenticate (make sure this matches the callback URL supplied in the OAuath object creation at the top of your app, though it does not have to match what you registered as your callback URL on Twitter), also passing along some unique credentials like candy for your app to nom nom on:

	app.get('/auth/twitter/callback', function(req, res, next){
		if (req.session.oauth) {
			req.session.oauth.verifier = req.query.oauth_verifier;
			var oauth = req.session.oauth;
	
			oa.getOAuthAccessToken(oauth.token,oauth.token_secret,oauth.verifier, 
			function(error, oauth_access_token, oauth_access_token_secret, results){
				if (error){
					console.log(error);
					res.send("yeah something broke.");
				} else {
					req.session.oauth.access_token = oauth_access_token;
					req.session.oauth,access_token_secret = oauth_access_token_secret;
					console.log(results);
					res.send("worked. nice one.");
				}
			}
			);
		} else
			next(new Error("you're not supposed to be here."))
	});

Now I'm sure you'll want to replace all the console logging and res sending with some cool templating magic (I suggest [EJS]), but otherwise, you should be good to go. Have fun.

Reference Gists:

- https://gist.github.com/555607
- http://stackoverflow.com/questions/5428745/problems-with-oauth-on-node-js

[Node.js]: http://nodejs.org
[node-oauth]: https://github.com/ciaranj/node-oauth
[devtwitter]: https:/dev.twitter.com/apps
[ExpressJS]: http://expressjs.com/ 
[EJS]: http://embeddedjs.com/