---
layout: post
title:      "Sinatra CMS Project"
date:       2019-05-12 19:24:01 +0000
permalink:  sinatra_cms_project
---


The task for this project was to create a CMS web-app using sinatra and other concepts we've learned so far.  These include using ActiveRecord and ORM, using an MVC file system, multiple ralated tables (has_many, belongs_to, has and belongs to many) and developing proficiency with github.

For this project I lazily took the suggestion of video games, however, that turned out to give me a lot to work with.  My project Allows the creation and editing of Users, Games, Developers and genres and supports views for each showing their relationships to one another. [table relationships](https://drive.google.com/file/d/16VENEUOnd_DGnfK39h7qvtxK3ifBXqew/view?usp=sharing) (eg. a game belongs to a developer, but can belong to many users and genres, Users have genres and developers through games). 

Not content to just write some basic seed data I looked into the Steam WebApi for getting more info, luckily a ruby [wrapper](https://github.com/Olgagr/steam-web-api) had been written for said api.  Unfortunately The steam api doesnt really like to give very much information so I went back to what we learned in the previous project and ended up using [nokogiri](https://nokogiri.org) to scrape more information until I was satisfied.

The finished project contains a large amount of seeded information for users to play with and three initial users with information pulled from their steam accounts.  New users can be created, pre-existing games can be added to accounts or new ones can be entered along with thier developers and genres. (steam is not necessary it just had a large amount of info to pull from).

It was another fun project where being left to ones own devices and starting from scratch gives invaluable information.  Tools like tux and pry where invaluable for digging into the program and seeing where things went wrong.  As well as shotgun for seeing what happens while navigating through the web app.

Short video demonstration [here](https://drive.google.com/file/d/19IHS_6TFyMFCp80L02U07OaAY1tBTeOE/view?usp=sharing)
