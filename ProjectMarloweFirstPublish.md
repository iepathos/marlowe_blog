# Project Marlowe - First Publish

Ok, the chrome extension frontend for the marlowe objectivity project has been through some testing and improvement.  It isn't perfect or pretty yet, but it works and that means get it out there in front of people to start gathering some more feedback.  I think its ready to be published up on the chrome app store for public consumption.  Time to go through the Google Chrome developer information and get it up there.  After that, going to signup on AMO and publish the Firefox extension.


Submitted both extensions, waiting for review on the Firefox submission, chrome one went through right away after paying the Chrome Web Store Developer fee of $5.00.  Submitted both extensions as version 0.5 where they take an average of the scores returned by microservices.  I was thinking I may actually want to take the lowest score out of all the scores returned, but haven't decided if that's the way to go yet.  Next I want to setup another backend objectivity microservice that uses a TextBlob, NaiveBayes and a custom dataset specifically for determining subjective vs objective sentences.  I think I will setup the new dataset as a separate repo and submodule that way it'll be easy to get at for any neural network or other machine learning approaches we add to this going forward.


## Dataset Setup

The format to use here is pretty straightforward.  Going to use a json file with this format:

````javascript
[
    {"text": "Because many of the decisions we made are subjective, there is the possibility of human error in our data set.", "label": "subjective"},
    {"text": "Roses are red.", "label": "objective"},
]
````

The tricky part here is finding good examples.  The classifiers we train off of it can be improved in various ways, but ultimately their performance relies heavily on the quality of the dataset.  Good data is essential for good machine learning performance.