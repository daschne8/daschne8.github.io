---
layout: post
title:      "Reddit Text Analyzer React Final Project"
date:       2019-08-07 18:46:34 +0000
permalink:  reddit_text_analyzer_react_final_project
---

For my Final project I wanted to see what fun API's where out there to play around with. With all the advances in AI, Machine Learning, Neural networks etc there are some neat toys out there.  I ended up choosing IBM Watson's tone analyser.  It takes text and can try to pick out a number of parameters while also being free up to a certain limit(this was a very important factor ;) ).
 
So I had my toy picked out but what text was I going to feed it?  Enter Reddit, "Front page of the internet" Lots of comments to sift through on every topic you could imagine make it a goldmine for analysis, I just wish it's API gave you more power than it does as I relized the limitations about halfway through my project. 

The end result is a project that allows a user to enter either a user or a subreddit from reddit as a query that will take a list of the most recent comments and feed it through the tone analyser.  The user can then see a snapshot of the multiple keywords/phrases and the emotions related to them and also the overal emotion at the time.  As well as allowing comparisons between queries.

The project is a combination of a Rails API that does the calls on the backend taking the reddit query and feeding its data to watson then posting the watson data back to the React front end.  React will display the data in tables and graphs for the user to peruse.  Originaly i had plans to show emotions over time of a given user/subreddit and pick out the associated keywords but unfortunalty the reddit api doesn't make this easy.  It dissalows searching by date and rate limits requests(one request every 2 seconds).  A longer term analysis would take a while to display and had to be scrapped in favor of a current snapshot model.

The project utilizes Rails, React, Redux, thunk, the reddit api, the watson api, and multiple other third party libraries.  React handles routing with data persisting between page changes and displaying said data.  The Rails backed is fairly simple and  I almost feel dirty after having learned so much about Rails to leave it as simple as it is but there wasn't much it needed to do and I see no reason to bloat or complicate things, it takes the request and gives the data.  

In the end I created a nice little functional react app, that gives an interesting snapshot of data from a mileu of comments.  I didn't think too much of it myself till I had freinds entranced and playing with it for > 20  minutes so I must have done something right.  I would warn people not to take the data too seriously as the limitations on both APIs really limit getting a respectable sample size but it is enough to think about.

As always it's a blast to do these projects and everytime I do I solidify more knowledge, whether it's of the frameworks i'm currently using, best coding practices, using different API's, or just getting better at coding in general.  It's a blast to feel yourself grow and I can't wait to keep growing in the future.
