---
layout: page
title: "QVDev blog"
description: ""
---
{% include JB/setup %}

Here will come my blog hosted on GitHub and powered by jekyll.

<ul >
    {% for post in site.posts limit 4 %}
    <li><span>{{ post.title }} &raquo; {{ post.date | date_to_string }}</span></li>
        {{ post.content | strip_html | truncatewords:75}}<br><br>
            <a href="{{ post.url }}">Read more...</a><br><br>
    {% endfor %}
</ul>