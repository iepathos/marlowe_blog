# Project Marlowe - Alpha Testing and Feedback


I ended up not publishing to the public yet on this, I wanted some quick feedbck first so I packaged up the extension and shared it around with some alpha testers.  After finding and fixing a bug with the rounding thanks to one of the testers, the main feedback I received was a couple testers being able to fool the objectivity check.  So, they would provide a clearly subjective sentence made up of words that the TextBlob classifier had never seen and it would think it was an objective sentence.

The objectivity from TextBlob is too limited, partly from its method and partly from its training dataset which is nltk corpus movie reviews.  I scouted around and found this [https://github.com/nik0spapp/usent](https://github.com/nik0spapp/usent) which looks like it suits my needs and I found generally better scores coming back from a wider variety of text input.  Options are to gut marlowe_objectivity and completely change it to use usent or I could add on this new method as a new service, and not even touch the existing marlowe_objectivity.  I see some sentences that are missed by one method but not the other so I think the best approach here is to start building out an ensemble of machine learning objectivity services to determine the objectivity of given text.  This'll be better down the line to start setting it up like this too as I find new methods for determine objectivity of text I can add them as new services in the cloud and then just add the url for the new services to the frontend applications.

Building out the usent service is going to be pretty quick because we have the usent library built and open source already and we have our existing marlowe_objectivity app.  usent seems to work best with Python 2.7.3 so going to take a copy of the marlowe_objectivity app, start new repository, add as submodule to devops repo, adjust the Dockerfile to take care of the installation requirements for usent, hack on usent a little bit for a separate objectivity function, and deploy to a new heroku instance.  Then on the frontend chrome extension, going to add a new function to post to the new marlowe_usent service on heroku and take an average between the two methods to determine objectivity of given text.  Need to make sure to build the frontend portion scalable, so that it's easy to add new services to check objectivity with just a url.


Ok, setting up the new marlowe_usent code is done after some 30 minutes of hacking, now I need to setup the wercker testing and deployment pipeline for it and deploy to heroku.  After some effort, realized Heroku doesn't want to deploy marlowe_usent because it limits boot time to 60 seconds and with the PyML build and install it exceeds that time limit. Fortunately, the parts of library I'm using don't really seem to need the PyML dependency so I've worked that out of it entirely and setup an nltk.txt file so heroku conveniently provides access to those datasets for my app without the extra download and install step in building.


Made the changes to the frontend chrome extension to post to both services and take an average of the sum of the scores from the objectivity apis.  Now if we add any new objectivity apis in the future it'll be as easy as adding a url for the frontend to connect it.  Sent out Marlowe Objectivity Extension v0.4 to alpha testers for more feedback with the improved objectivity api.