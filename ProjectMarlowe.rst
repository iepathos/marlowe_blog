# Project Marlowe - Introduction

I'm going to build a web service and various client applications to help fix bad news.  I plan to openly blog about it while I build it here.  This is a side project for me.  Given the state of journalism these days, it has risen quickly on my priority list for side projects.  First thing is first, going to use a microservices architecture because I'm good with devops, so a lot of the complexity involved in microservice architectures I can reduce with automation so that the downsides are minimised while we have the potential to reap the benefits.  Some of the benefits include, increased modularity and adaptibility.


### Initial Components

+ Objectivity JSON API - Send text, get objectivity score
    - Docker Container for Python 3.6

+ Chrome Extension - Get objectivity score of text

+ Firefox Extension - Get objectivity score of text


### Secondary Components

+ Political Bias JSON API - Send text, get political bias (will probably need to build out custom neural network and training for this)

+ Chrome Extension - Get Political Bias

+ Firefox Extension - Get Political Bias


## Getting Started - Objectivity API

I setup a master repo which is the devops and I add any microservice to it as a git submodule.  Using github for the source hosting for this project.  I intend to do the whole project open source.  I use a separate git repository for each submodule.  I've seen some attempts at microservice architecture get this wrong.  Making sure the various services are using different repos makes it a lot easier when setting up the continuous integration which already has its tools based around watching changes and building individual repositories.  So, at this point I setup the [marlowe_blog](https://github.com/iepathos/marlowe_blog) submodule which just contains this post so far.  I set that up inside of a devops repo [marlowe_devops](https://github.com/iepathos/marlowe_devops).  


Ok, next step is to build out the objectivity api.  The open source library [TextBlob](https://textblob.readthedocs.io/en/dev/) already provides a quick method to get a general subjectivity score from text.  I think it uses NaiveBayes model to determine subjectivity, may want to improve upon this later, but it's a great starting point and it's ready to go.  Objecitivty is the opposite of subjectivity so I'm going to say: objectivity = 1 - subjectivity.  I setup flask to quickly setup a simple server to receive text and return an objectivity score.  Then I wrapped that server inside of a docker container and setup a docker-compose.yml so I can use docker-compose for local development and testing.  Then I built out a basic unit test for it, found a bug to fix and added an example curl call.  [marlowe_objectivity](https://github.com/iepathos/marlowe_objectivity) Going to come back later to improve how this service determines objectivity over large portions of text, but for now this api is good to go development wise.  Time to setup a continuous integration workflow for it all the way to production, then I'll have maybe the world's first objectivity api in production with 1 user, me.


Going to use wercker since I'm doing this project open source.  If this were a larger project, I think I would prefer setting up a Jenkins server.  Wercker setup for the objectivity service, added readme to the service with wercker badge so testing status is easily visible.  [wercker marlowe_objectivity](https://app.wercker.com/iepathos/marlowe_objectivity)


Next step is to choose how to host this service and then setup a wercker deployment step to deploy to host if tests pass ok.  Options I'm considering are AWS EC2, AWS Lambda, Google Cloud, Digital Ocean, Heroku, and Linode.  Some of them I'm very familiar with and others I'm just interested in trying out.  Heroku's free tier should be sufficient for my needs initially and I can easily switch that to a Dokku setup on AWS EC2 or Linode afterward if I need to scale up.  Wercker already has a heroku-deploy step which is straight forward to use.

Ok, we have an API in production on Heroku with Wercker handling continuous integration openly for the public to view the deployment workflow.  All devs have to do is code and push to github now for the development workflow to kick in.  This open source project is off to a great start.


## Chrome Extension

This is going to be my very first time building a browser extension.  Pretty excited about it, found [this little tutorial](https://www.sitepoint.com/create-chrome-extension-10-minutes-flat/) to get started with and everything seems like it's pretty much going to be HTML, CSS, and Javascript.  First thing, setup new repository and submodule for any extension code within the base [marlowe_devops](https://github.com/iepathos/marlowe_devops) repository.  I built out the chrome extension here [marlowe_chrome](https://github.com/iepathos/marlowe_chrome).  It is very minimal so far using a popup with text input and button to post to the Marlowe API and return the objectivity score.  Will likely improve this setup later for a more highlight and right click setup rather than this popup copy paste setup.  Starting out basic with it and moving along for now.  Added a right click context menu background function so that users can just right click to check the objectivity of highlighted text.

Next step is to package this extension and get it up on the store so we can get it in production.


## Firefox Extension






