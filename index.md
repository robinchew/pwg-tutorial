---
layout: page
title: Developer's Guide!
---

{% include JB/setup %}

Notes for a Clojurescript Beginner
==================================

Learning Clojure itself is pretty nice, but learning the libraries and frameworks built for Clojurescript through Google is fucking painful, so here's some notes.

Boot
----

By default boot will compile to **target/main.js**. Say you want to change to **static/everything.js**, you need to set build.boot correctly and put the edn in the right place:

build.boot

    (set-env! :target-path "static"
              :source-paths #{"src"}
              :dependencies '[...])

src/everything.cljs.edn

    {:require [myproject.app]}

Your directory structure would look like:

    root
    ├── build.boot
    └── src
        ├── myproject
        │   └── app.cljs
        └── everything.cljs.edn

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
