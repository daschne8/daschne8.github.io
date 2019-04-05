---
layout: post
title:      "Writing the Ruby CLI"
date:       2019-04-05 16:55:15 +0000
permalink:  writing_the_ruby_cli
---


It was definatly a change having to go from structured labs that take you step by step through making a program and being left completely to your own devices but I can say I loved the freedom!  I feel like you learn a lot more when you start from the bottom and have to build the pieces yourself.

This project was mostly for us to demonstrate our knowledge of Object Oriented design principles, unfortunatly I didn't get to show off everything we learned (Looking back over my code I didn't even end up using Inheritance) and I didn't feel like shoehorning it in unecessarily.  I chose a subject, in this case travel, and I chose a website, Kayak, and just went with it.

![Screenshot of program](https://drive.google.com/file/d/1q-VKpssKAoG1dT0lzCPwTnNOZQf2oTlf/view?usp=sharing)

The cli pulls from a list of three travel destinations from kayak from airports near you, you are then able to select more info about a travel destination and from there to see a list of information about flights to said location.

While trying to scrape the data about flights I learned that the page is dynamically loaded and uses AJAX and instead of just choosing a new website I figured this is a great time to learn more.  Nokogiri will only read the initial html from a page and is unable to help here as the html is not loaded all at once.  I found a work around with ruby Watir gem, however while using a method to wait for an element to appear on a page KAYAK blocked me for being a bot. After waiting a day to have access again I had to resort to a simple #sleep call to load the page and get all the information.

Aside from practicing coding skills while doing this project I also had to learn how to setup my own Ubuntu VM, how to use Ubuntu, How to use the command line and git, using the Google chrome browser to inspect webpages and i'm sure more i'm forgetting.

Overall I learned a lot both about coding and the environment around it, using google and documentation to learn about new gems, errors, general coding practices and the like.  It was fun and i can't wait for the next one.



