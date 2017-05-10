# ProjectMarloweNewDataset

I'm not very satisfied with the existing open source subjectivity/objectivity dataset. It comes from movie reviews and provides 5000 sentences objective and 5000 subjective sentences.  There isn't anything particularly wrong with it, but for the purposes of this project, I think a much larger dataset is required to improve the accuracy of the underlying machine learning microservices that are trained on it.  After this new dataset is setup, I can setup a third machine learning microservice that uses the new dataset to classify text and add it to existing Objectivty ensemble.

I want to systematically harvest to create a new objective/subjective dataset.  The reddit comments dataset is huge and probably a good place for subjective sentences, but I don't want to let a bunch of objective sentences slip through so I'm going to run any sentences I harvest from it through the existing classifiers I have setup.  Low scores can be added to the subjective data, middle scores will be excluded and high scores can go into the objective data.  Objective sentences are harder, but I think I can gather a goodly amount if I scrape some scientific journals and news sources and run them through the existing classifiers for high scoring sentences.

Ideally, a human can go over the data afterward and weed out any outliers, but that's a time intensive task that I can't commit to currently.  This is an open source project, so hopefully if anyone else out there uses it and is trying to help out they can remove bad data and send a pull request.



Downloading the 8 GB reddit comments json takes a little while.  It is 1.7 billion comments, now that's some real data, not a measely 10k.  I'm setting up a script in the dataset repository to handle parsing the comments and then checking their score with the existing services.  Going to query services locally with it and buildout a docker-compose.yml in the base devops repo that will spin up the two services on different ports and then call the reddit parse script to use those services.
