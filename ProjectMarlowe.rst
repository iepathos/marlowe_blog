I'm going to build a web service and various client applications to help fix bad news.  I plan to openly blog about it while I build it here.  This is a side project for me.  Given the state of journalism these days, it has risen quickly on my priority list for side projects.  First thing is first, going to use a microservices architecture because I'm good with devops, so a lot of the complexity involved in microservice architectures I can reduce with automation so that the downsides are minimised while we have the potential to reap the benefits.  Some of the benefits include, increased modularity and adaptibility.

Objectivity JSON API - Send text, get objectivity score
    - Docker Container for Python 3.6

Chrome Extension - Get objectivity score of text

Firefox Extension - Get objectivity score of text



I setup a master repo which is the devops and I add any microservice to it as a git submodule.  Using github for our host for this open source project.  I use a separate git repository for each submodule.  I've seen some attempts at microservice architecture get this wrong.  Making sure the various services are using difference repos makes it a lot easier when setting up the continuous integration which already has its tools based around watching changes and building individual repositories.  So, at this point I setup the [marlowe_blog](https://github.com/iepathos/marlowe_blog) submodule which will just contain posts I write like this one.  I set that up inside of a devops repo [marlowe_devops](https://github.com/iepathos/marlowe_devops).  


Ok, next step is to build out the objectivity api.  The open source library [TextBlob](https://textblob.readthedocs.io/en/dev/) already provides a quick method to get a general subjectivity of some text.  Objecitivty is the opposite of subjectivity so we're going to say given if a score has, for instance, a score .2 subjectivity, the text would have .8 objectivity score.  Going to use flask to quickly setup a simple server to receive text and return an objectivity score.  Then I am going to wrap that server inside of a docker container.  Have a nice simple service going now with a minimal docker setup.  Built the unit test for it, found a bug to fix and added an example curl call.  [marlowe_objectivity](https://github.com/iepathos/marlowe_objectivity) Going to come back later to improve how this service determines objectivity over large portions of text, but for now this api is good to go development wise.  Time to setup a continuous integration flow for it all the way to production, then I'll have maybe the world's first objectivity api in production.