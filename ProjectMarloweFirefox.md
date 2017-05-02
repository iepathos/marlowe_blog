# Project Marlowe - Firefox Extension

Ok, we have two objectivity methods wrapped into docker flask microservices up in the heroku cloud for free.  Our deployments to those services are entirely automated by wercker.  Everything is hosted on github and is open source.  


Now to setup the Firefox extension, I want to utilize most of the existing code in the Chrome extension.  After searching about I found this for porting a Chrome extension to Firefox [https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Porting_a_Google_Chrome_extension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Porting_a_Google_Chrome_extension).  So, going through this little tutorial now.  

Pretty straight forward, ended up being able to use the code for the Chrome extension with minimal changes.  One thing I had to add to the backend services was flask-cors so that the CORS header is attached to requests, firefox didn't like that the header was missing.  Firefox also blocked using alert() from the background script, but I was able to hack around this problem using browser.tabs.executeScript() to get it to work.  Also, found a bug if None was returned by the text field on the servers and patched that with a simple check.

Ready to publish the Firefox Marlowe Objectivity Extension and share it around for more testing and feedback.


Please see the next post ProjectMarloweFirstPublish.md