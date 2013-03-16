---
date: 2013-01-05 09:14:00 +1000
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
Cloudbees account. Also posible to use youre google account.<br>
Github account with a public repository. Private is posible too, but will discus later.<br>
<br>
Step one:<br>
Setup your cloubees account and go to builds.<br>
<br>
Step two:<br>
Enter a job name and select "Build a free-style software project" and hit OK.<br>
<br>
Step three:<br>
Fill in the following:<br>
<br>
At Source Code Management choose Git and enter you're repository.<br>
for example:<br>
{% highlight objective-c %}
git://github.com/username/repository.git
{% endhighlight %}
<a href="/assets/images/img3.png" target="_blank"><img src="/assets/images/img3.png" alt="" width="75%" height="75%"></a>
At Build do the following:<br>
Add build step and choose Execute shell.<br>
Enter the following in the box:<br>
{% highlight objective-c %}
#generate the local.properties file
    rm -f local.properties
    $ANDROID_HOME/tools/android update project --path ./
{% endhighlight %}
Then add another build step but this time choose:<br>
Invoke Ant and enter the preferred ant builds. For now just type:
{% highlight objective-c %}
clean debug
{% endhighlight %}
Now on the right choose advanced and setup the build.xml file. Normally this is in the root of the project so enter there:
{% highlight objective-c %}
build.xml
{% endhighlight %}
<a href="/assets/images/img2.png" target="_blank"><img src="/assets/images/img2.png" alt="" width="75%" height="75%"></a>
<br>
//Side note If you have not configured your Android project for Ant build see the following website how to setup 
your project for ANT.<br>
<a href="http://www.androidengineer.com/2010/06/using-ant-to-automate-building-android.html">http://www.androidengineer.com/2010/06/using-ant-to-automate-building-android.html</a><br>

Final step:<br>
Then presse Apply and Save. This will bring you back to you're job. Now all you have to do is choose build 
now and you are done!

When the build is successful you can find back the debug .APK that Jenkins has generated, 
go to workspace and choose bin. project.APK.
<a href="/assets/images/img1.png" target="_blank"><img src="/assets/images/img1.png" alt="" width="75%" height="75%"></a>
<!-- more end --> 
