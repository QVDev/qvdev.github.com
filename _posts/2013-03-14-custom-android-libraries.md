---
layout: post
title: "Custom Android Libraries"
description: ""
category: "android"
comments: true
tags: ["android, libraries"]
---
{% include JB/setup %}

<br>
Started playing around creating libraries for Android. The first useful library I made is a custom ListView and GridView. 
The purpose is to have some animation to indicate the top or bottom of the scrolling. 
To use it add the .jar file to you're libraries can be downloaded at the bottom, and define you're xml layout as follow: 
<!-- more start -->
{% highlight java %}
//ListView
qvdev.utils.libraries.lists.KinecticListView ...
//GridView
qvdev.utils.libraries.lists.KinecticGridView ...
{% endhighlight %}
And then in in code you can do simply the following. 
{% highlight java %}
private void test()
{
 mListContent = (KinecticListView) findViewById(R.id.content_list);
 mListContent.setAdapter(mListAdapter);
        mListContent.setBouncing(true); //For bouncing animation
        mListContent.setKinectic(true); //For kinectic animation      
}
{% endhighlight %}
Source code can be found here: <a href="https://github.com/QVDev/QVListLibraries/" target="_blank">QVListLibraries on GitHub</a>
<!-- more end -->