# Your Garden of Om

This book assumes at least you've taken a
[quick](https://github.com/clojure/clojurescript/wiki/Rationale) 
[peek](http://clojurescriptkoans.com/) at
[clojurescript](https://github.com/clojure/clojurescript) or clojure.

Also it is assumed that you have [Leinengen](http://leiningen.org/) installed
and will now run this from your shell:

```shell
lein new mies-om grok-om
cd grok-om
lein cljsbuild auto grok-om
```

Thus your garden should spring to life:

> ```bash
Compiling ClojureScript.
Compiling "grok_om.js" from ["src"]...
Successfully compiled "grok_om.js" in 8.256 seconds.
```

The two files to open now are **index.html** in your browser
and **src/grok_om.cljs** in an editor. 

In your editor, delete everything after `(enable-console-print!)`.

Any changes you save to the .cljs source will trigger project recompilation by cljsbuild.

> I recommend using a tool like [LiveReload](http://livereload.com/) to refresh your browser when the
> contents of the project folder are changed. No manual browser refreshing.
> I also suggest now as a good time to go grab a tea or coffee.

![](http://rlv.zcache.com/clojure_mug_i_get_more_done_when_im_lazy_v2-r8a645a385b434050b5474ac17fc27ddb_x7jsg_8byvr_324.jpg)
