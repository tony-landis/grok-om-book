# Foundation CSS Framework

The components created (mostly) make use of the [Foundation CSS](http://foundation.zurb.com/docs/) framework.
The resulting collection of components benefit from the existing Foundation
styling without any dependancy on the Foundation framework javascripts.

The finished Foundation components have their own github repository:
https://github.com/tony-landis/om-foundation

> We'll wind up with something like this, except for Om instead of Angular:
> http://madmimi.github.io/angular-foundation/


## Adding new project dependencies

* [anka](https://github.com/noprompt/ankha)   &ndash; a generica data inspection component
* [ŜABLONO](https://github.com/r0man/sablono) &ndash;  hiccup style templating for Om/React

Update the `:dependencies` key in `project.clj` to:

```
:dependencies [[org.clojure/clojure "1.5.1"]
               [org.clojure/clojurescript "0.0-2173"]
               [org.clojure/core.async "0.1.267.0-0d7780-alpha"]
               [om "0.5.0"]
               [ankha "0.1.2"]
               [sablono "0.2.16"]]
```

You will need to restart lein in order to pickup the new deps:

```shell
lein cljsbuild auto grok-om
```


## Updating index.html

The default include for react.js in index.html has a redirect that drasticly slows down page reload.
Lets fix that, add the foundation css include, and add a new root dom node that we'll need later.

Open `index.html` and change it to:

```html
  <head>
    <link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/foundation/5.2.2/css/normalize.min.css">
    <link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/foundation/5.2.2/css/foundation.min.css">
  </head>
  <body>
    <div id="app"></div>
    <div id="debug"></div>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/react/0.10.0/react.js" type="text/javascript"></script>
    <script src="out/goog/base.js" type="text/javascript"></script>
    <script src="grok_om.js" type="text/javascript"></script>
    <script type="text/javascript">goog.require("grok_om.core");</script>
  </body>
</html>
```


![](http://foundation.zurb.com/assets/img/homepage/hero-image.svg)
