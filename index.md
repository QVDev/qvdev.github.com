---
layout: page
title: "QVDev blog"
description: ""
---
{% include JB/setup %}
<ul >
    {% for post in site.posts limit 10 %}
    <li><u><b><a href="{{ post.url }}">{{ post.title }}</a></b></u> &raquo; <span class="post-date"> {{ post.date | date_to_string }} tags:{{post.tags}}</span></li>
        <span class="preview-content">{{ post.content | replace:'more start -->','' | replace:'<!-- more end',''}}</span>            
    {% endfor %}
</ul>