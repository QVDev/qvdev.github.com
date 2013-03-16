---
date: 3013-01-05 09:14:00 +1000
layout: post
title: "Continuous integration with Jenkins"
category: "android"
comments: true
tags: ["android, jenkins, continous integration"]
---
{% include JB/setup %}
<br>
Recently I looked into continuous integration for Android applications, that I hosted on Github. 
After some research cloudbees.com caught my interest. Here I will shortly describe how to set this up in about 15 minutes.
<br><br>
<!-- more start -->
Prerequisite:
Cloudbees account. Also posible to use youre google account.
Github account with a public repository. Private is posible too, but will discus later.

Step one:
Setup your cloubees account and go to builds.

Step two:
Enter a job name and select "Build a free-style software project" and hit OK.

Step three:
Fill in the following:

At Source Code Management choose Git and enter you're repository.
for example:
<!-- more end --> 
