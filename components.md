# Om Components

Om recycles the term "**component**" from Facebook React.

> Visualize the component as a reactive interface with state.

A component has no data model binding specified.

Until called, a component has has no parent component binding.

These properties enable reusability, composability, and the elimination of external boilerplate.

![](http://tilings.math.uni-bielefeld.de/Files/Disconnected_2_Rauzy_03_sm.gif)

At a minimum, components must implement `IRender` or `IRenderState`,
 both will be explained later. 

Add this useless component to core.cljs:

```clojure
(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/h1 nil "Hello World!"))))
```

Next, Let's get this into the DOM.
