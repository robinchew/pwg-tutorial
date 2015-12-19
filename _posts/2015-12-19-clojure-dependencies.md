Clojure Dependencies
====================

No matter if you use lein or boot, every dependency version, no matter how minor, must be handled with care. Not only must you get one package version right, you must get the combination of multiple libraries with the right version, or else BOOM!. Actually the errors aren't as obvious as a boom, the errors are so unhelpful that you don't know if you configured incorrectly or it's really a version problem.

At least the following build.boot works for me as a vim user with the ability to do inline evaluation.

```clojure
(set-env!
  :target-path "static"
  :source-paths #{"src/cljs"}
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
                  [pandeiro/boot-http "0.7.1-SNAPSHOT"]
                  ])
(require
  '[adzerk.boot-cljs :refer :all]
  '[adzerk.boot-cljs-repl :refer [cljs-repl start-repl]]
  '[adzerk.boot-reload :refer [reload]]
  '[pandeiro.boot-http :refer [serve]])

(deftask run []
  (comp (serve)
        (watch)
        (cljs-repl)
        (reload)
        (cljs)))

(deftask production []
  (task-options! cljs {:output-to "static/cloject.js"
                       :optimizations :advanced})
  identity)

(deftask development []
  (task-options! cljs {:output-to "static/cloject.js"
                       :optimizations :none :source-map true}
                 reload {:on-jsload 'cloject.main/main})
  identity)

(deftask dev
  "Simple alias to run application in development mode"
  []
  (comp (development)
        (run)))

```
