---
layout: post
title: Change Clojure Boot target
---

{% include JB/setup %}

Changing Clojure Boot Target
============================

In lein, you would be familiar with the **output-to** build setting. It's not as straight forward to change that in boot.

By default boot will compile to **target/main.js**. Say you want to change to **static/everything.js**, you need to set build.boot correctly and put the edn in the right place:

build.boot - The key things to look at are **target-path** and **source-paths*. I'm showing you the dependencies so you get the versions right.

    (set-env! :target-path "static"
              :source-paths #{"src"}
              :dependencies '[[org.clojure/clojure "1.7.0"]
                              [org.clojure/clojurescript "1.7.170" :scope "provided"]
                              [org.clojure/core.async "0.1.346.0-17112a-alpha"]
                              [com.cemerick/piggieback "0.2.1"  :scope "test"]
                              [weasel "0.7.0"  :scope "test"]
                              [cljs-ajax "0.3.14"]
                              [datascript "0.13.3"]
                              [funcool/cuerdas "0.6.0"]
                              [reagent "0.5.1"]
                              [adzerk/boot-cljs "1.7.170-3" :scope "test"]
                              [adzerk/boot-cljs-repl   "0.3.0"]
                              [adzerk/boot-reload "0.4.2" :scope "test"]
                              [pandeiro/boot-http "0.7.1-SNAPSHOT"])

src/everything.cljs.edn

    {:require [myproject.app]}

Your directory structure would look like:

    root
    ├── build.boot
    └── src
        ├── myproject
        │   └── app.cljs
        └── everything.cljs.edn
