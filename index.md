---
layout: page
title: Hello World!
tagline: Under Construction since 1999
---
{% include JB/setup %}

So yeah... more should go here one day... but that day is not today.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



