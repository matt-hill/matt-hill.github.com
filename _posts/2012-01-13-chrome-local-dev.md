---
layout: default
title: Chrome 
tags: [ chrome, ajax, backbonejs ]
---

Over the last year, I've migrated completely off Firefox and Safari, and use Chrome pretty much all the time now. So obviously, all my development is in Chrome as well. While this is typically ideal, I've recently started working with [Backbone.js] and have run into a reasonable ( security related ) but annoying issue wherein Chrome will not allow me to load local files via AJAX.

	XMLHttpRequest cannot load file://localhost/Users/me/repos/app/templates/blah.html. Cross origin requests are only supported for HTTP.
	js/libs/text.js:7Uncaught Error: NETWORK_ERR: XMLHttpRequest Exception 101
	
Look familiar? Well, this has been locking me into a pattern of stacking my templates in the main HTML file which tonight I finally had enough of, so I tracked down the info needed to create an OSX dock icon to load Chrome with the right arguments to disable this feature so that when I'm developing I can start Chrome via this method instead, allowing me to load files via AJAX all day long. And there was much rejoicing.

Step 1. Open the AppleScript editor ( Applications > Utilities > AppleScript Editor )

Step 2. Paste this line into the editor:

	do shell script "open '/Applications/Google Chrome.app' --new --args -allow-file-access-from-files"

Step 3. Click Compile.

Step 4. While in the editor, File > Save As > 'ChromeDev'. Make sure the file format is 'Application'.

Step 5. Open your finder window to wherever you saved the compiled script and drag it to our dock.

Step 6. Have fun with local AJAX calls

[Backbone.js]: http://documentcloud.github.com/backbone/