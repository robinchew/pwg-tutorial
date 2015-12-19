---
layout: post
title: Clojure Dependencies
---

{% include JB/setup %}

Clojure Dependencies
====================

No matter if you use lein or boot, every dependency version, no matter how minor, must be handled with care. Not only must you get one package version right, you must get the combination of multiple libraries with the right version, or else BOOM!. Actually the errors aren't as obvious as a boom, the errors are so unhelpful that you don't know if you configured incorrectly or it's really a version problem.
