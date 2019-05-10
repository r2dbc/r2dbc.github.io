---
layout: page
title: Blog
permalink: /blog/
---

<ul>
  {% for post in site.posts %}
    <li>
      {{ post.date | date: "%Y-%m-%d" }} - <a href="{{ post.url | split: ".html" }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>