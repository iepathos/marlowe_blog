I'm going to build a web service and various client applications to help fix bad news.  I plan to openly blog about it while I build it here.  This is a side project for me.  Given the state of journalism these days, it has risen quickly on my priority list for side projects.  First thing is first, going to use a microservices architecture because I'm good with devops, so a lot of the complexity involved in microservice architectures I can reduce with automation so that the downsides are minimised while we have the potential to reap the benefits.  Some of the benefits include, increased modularity and adaptibility.

Objectivity JSON API - Send text, get objectivity score
    - Docker Container for Python 3.6

Chrome Extension - Get objectivity score of text

Firefox Extension - Get objectivity score of text



I setup a master repo which is the devops and I add any microservice to it as a git submodule.  Using github for our host for this open source project.  I use a separate git repository for each submodule.  I've seen some attempts at microservice architecture get this wrong.  Making sure the various services are using difference repos makes it a lot easier when setting up the continuous integration which already has its tools based around watching changes and building individual repositories.  So, at this point I setup the [marlowe_blog](https://github.com/iepathos/marlowe_blog) submodule which will just contain posts I write like this one.  I set that up inside of a devops repo [marlowe_devops](https://github.com/iepathos/marlowe_devops).  


Ok, next step is to build out the objectivity api.

