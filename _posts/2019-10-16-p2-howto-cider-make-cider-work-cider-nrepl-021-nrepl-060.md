---

layout: post
title: "How to make cider work in project.clj: set dependencies to nrepl 0.6.0 and plugins for cider-nrepl to 0.21.1 "
---

# Pontifications

* Here's how I got cider to work in emacs as of today:
  * Set dependencies to nrepl 0.6.0:
    *  `:dependencies [[org.clojure/clojure "1.8.0"] [nrepl "0.6.0"]]`
  * Set plugins to cider-nrepl 0.21.1:
    *  `:plugins [[cider/cider-nrepl "0.21.1"]]`

# Full proj.clj

```clojure
(defproject clojure-noob "0.1.0-SNAPSHOT"
  :description "FIXME: write description"
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.8.0"] [nrepl "0.6.0"]]
  :main ^:skip-aot clojure-noob.core
  :target-path "target/%s"
  :plugins [[cider/cider-nrepl "0.21.1"]]
  :profiles {:uberjar {:aot :all}})
```

