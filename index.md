---
layout: page
title: "QVDev blog"
description: ""
---
{% include JB/setup %}
<ul >
    {% for post in site.posts %}
    <li><u><b><a href="{{ post.url }}">{{ post.title }}</a></b></u></li>
        <span class="preview-content">{{ post.content | replace:'more start -->','' | replace:'<!-- more end',''}}</span>            
    {% endfor %}
</ul>