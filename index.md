---
layout: page
title: "Developer's Guide"
published: true
---



{% include JB/setup %}

Notes for a Clojurescript Beginner
==================================

Learning Clojure itself is pretty nice, but learning the libraries and frameworks built for Clojurescript through Google is fucking painful, so here's some notes.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
