# App Layout

Not only will we be creating Foundation components,
but composing them into a layout that suitable for
an app with authentication, navigation, search, login, ... TODO

The first step will be to create a root component to setup the layout.
We'll build our other components out from there.

In `src/core.cljs` delete everything after `(enable-console-print!)` and update to:

```clojure
(defn app-layout [app owner]
  (reify 
    om/IRenderState 
    (render-state [_ state]
      (html [:div
             [:div#top-bar 
              [:h1 "top bar goes here" ]]
             [:div#off-canvas 
              [:h3 "off canvas goes here"]]]))))

(om/root app-layout app-state {:target (. js/document (getElementById "app"))})
```


## TODO

* explain :require sablono and ankha

