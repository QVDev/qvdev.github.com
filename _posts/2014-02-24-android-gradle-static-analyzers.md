---
date: 2014-02-24 14:00:00 +1000
layout: post
title: "Android Gradle Static analyzers"
description: ""
category: "android"
comments: true
tags: ["android, gradle, static, analyzers"]
---
{% include JB/setup %}
<br>
To make sure you're code is good quality there are several static anaylyzers out there you can make use of. 
In this post I will highlight the most popular ones. I will show you how to configure them for you're Android
project that make use of the Gradle build system. On the internet I could not found alot about how to
configure this, so I thought it might be usefull to share this with other developers.
<br>
The following static analyzers I will discuss.<br><br>
<b>Checkstyle</b><br>
<b>PMD</b><br>
<b>Findbugs</b><br>
<b>CodeNarc</b><br>
<br>
In this post, CI setup will not be discussed, if need and wanted I can make a follow up post about how to
configure a CI system to report the analytics.<br><br>
<!-- more start -->
<b>So lets start:</b><br>
add the following to you're build.gradle file or just the one you want:
{% highlight groovy %}
apply plugin: 'checkstyle'
apply plugin: 'pmd'
apply plugin: 'findbugs'
apply plugin: 'codenarc'
{% endhighlight %}
This will just apply the plugins. To make sure they appear in the gradle tasks we need to add some more.
Add the following at the end of you're build.gradle file just the one(s) you want.<br><br><br>
<b>CheckStyle</b><br>
{% highlight groovy %}
task checkstyle(type: Checkstyle) {
	source 'src'
    include '**/*.java'
    exclude '**/gen/**'    
	// empty classpath
    classpath = files()
    //Do not fail build
    ignoreFailures = true
}
{% endhighlight %}
<b>PMD</b><br>
{% highlight groovy %}
task pmd(type: Pmd) {
    source 'src'
    include '**/*.java'
    exclude '**/gen/**'
    ruleSets = ["android"]
}
{% endhighlight %}
<b>Findbugs</b><br>
{% highlight groovy %}
task findbugs(type: FindBugs) {
    ignoreFailures = true
    classes = fileTree('build/classes/debug/')
    source = fileTree('src/main/java/')
    classpath = files()
    effort = 'max'
}
{% endhighlight %}
<b>Findbugs exclude filter</b><br>
{% highlight groovy %}
	tasks.withType(FindBugs) {
    excludeFilter = file("config/findbugs/excludeFilter.xml")
}
{% endhighlight %}
<b>CodeNarc</b><br>
{% highlight groovy %}
task codenarc(type: CodeNarc) {
    source 'src/main/java'
    configFile =  file("config/codenarc/codenarc.xml")
}
{% endhighlight %}
Now all tasks are configured and ready to be used. By using one of the following commands in you're terminal
or start them straight from Android Studio in the Gradle tasks right side bar.
{% highlight groovy %}
    gradle checkstyle
    gradle pmd
    gradle findbugs
    gradle codenarc
{% endhighlight %}
All of the reports can be found in the following directory:
{% highlight groovy %}
    /build/reports/(findbugs)/*.html/.xml
{% endhighlight %}
Of course this is just a setup. But from here you can configure the plugins to you're needs. Hopefully this
will help you to make you're code better quality. Please if you run into any problems or have feedback about the
blog post. Dont hesitate to leave them at the bottom of the page.
<!-- more end --> 
