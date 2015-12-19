Learn Clojure Boot
==================

I'm a messy learner. The way I lear boot is to just run:

    lein new tenzing your-app

That line came from a talk https://youtu.be/93CttPV79Q0?t=2043. You should probably watch it to get an idea of how boot works.

Tenzing is just the author's project name, just use it as a reference project that has a running boot, then tweak it to your liking. It's a roundabout way to setup boot since first you need **lein** (boot's competitor) then you pull in someone else's project with boot, just to get the server running on your project. This was my crude way of getting things setup with minimal reading and maximum copy pasting.

This is the **build.boot** that I end up with after making a number of changes for my own need. If it doesn't work for you, perhaps you should forget about my bulid.boot and just tinker with tenzing to fit your needs:

```clojure
(set-env!
  :target-path "static"
  :source-paths #{"src/cljs"}
  :dependencies '[[org.clojure/clojure "1.7.0"]
                  [org.clojure/clojurescript "1.7.170" :scope "provided"]
                  [com.cemerick/piggieback "0.2.1"  :scope "test"]
                  [weasel "0.7.0"  :scope "test"]
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
If I take piggieback out, I get an error when running ```boot dev```, but I need it anyway for inline evaluation in vim text editor. Weasel needs to be there because of piggieback I think, I don't know.

Here's my directory structure:

```
root
├── build.boot 
├── src
│   └── cljs
│       ├── cloject
│       │   └── main.cljs
│       └── cloject.cljs.edn
└── static
     └── cloject.js ('boot dev' generates this)
```
