---
layout: post
title: Contributing to a Minor Clojure Project
description: Adding to the ns-dep-graph Clojure plugin
date: 29/3/2016
---

I was bored the other day so I decided to work on improving this little Clojure plugin called ['ns-dep-graph.'](https://github.com/hilverd/lein-ns-dep-graph) It is what created [those Clojure dependency graphs](http://ssunday.github.io/2016/dependency-inversion-graph/). It was an intriguing piece of work, but there were some problems with it and some features to be added to really flesh it out. The ones I focused on were custom file naming and making it so when it generates a graph it does not overwrite a file with the same name and instead creates a new one. The latter issue was one I was frustrated with when using it. So I fixed it.

Here is the modified code that accomplishes both of these things:

```clojure
(defn- add-image-extension [name]
  (str name ".png"))

(defn- hash-user-arguments [args options]
  (try (apply hash-map args)
  (catch Exception e (do (println "WARNING: Optional argument missing a corresponding value. Defaulting."))
                          options)))

(defn- build-arguments [args]
  (let [options {"-name" "ns-dep-graph"}
        hashed-args (hash-user-arguments args options)
        valid-options (remove nil? (map #(find hashed-args (first %)) options))]
    (merge options (into {} (filter (comp some? val) valid-options)))))

(defn ns-dep-graph
  "Create a namespace dependency graph and save it as either ns-dep-graph or the supplied name."
  [project & args]
  (let [built-args (build-arguments args)
        file-name (get built-args "-name")
        source-files (apply set/union
                            (map (comp ns-find/find-clojure-sources-in-dir
                                       io/file)
                                 (project :source-paths)))
        tracker (ns-file/add-files {} source-files)
        dep-graph (tracker ::ns-track/deps)
        ns-names (set (map (comp second ns-file/read-file-ns-decl)
                           source-files))
        part-of-project? (partial contains? ns-names)
        nodes (filter part-of-project? (ns-dep/nodes dep-graph))]
      (loop [name file-name
             counter 1]
          (if (.exists (io/file (add-image-extension name)))
              (recur (str file-name counter) (inc counter))
              (viz/save-graph
               nodes
               #(filter part-of-project? (ns-dep/immediate-dependencies dep-graph %))
               :node->descriptor (fn [x] {:label x})
               :options {:dpi 72}
               :filename (add-image-extension name))))))
```

[Or you could just look at the github repo for it.](https://github.com/ssunday/lein-ns-dep-graph/blob/master/src/leiningen/ns_dep_graph.clj)

My changes weren't anything too major, but I *did* do it. I went a step further then just fixing it--I [created a pull request](https://github.com/hilverd/lein-ns-dep-graph/pull/4) to merge into the main repository. And, as one can see, it was merged. Cool. I contributed to another person's project. A first time ever on Github. Feels pretty good to have done that. Hope someone enjoys it.
