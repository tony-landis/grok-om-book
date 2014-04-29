# Component State

Unlike __application state__, which may be safely utilized across many components,
 __component state__ is contained only within the scope of a single component instance.

> App state has many
Using application state for data which is not needed outside of the scope and lifecycle of a single component may needlessly complicate an application.

![](http://ak9.picdn.net/shutterstock/videos/4986692/preview/stock-footage-barn-swallow-sitting-on-a-tree-branch-and-white-background.jpg)


---

Let's build a Component that accesses and updates Component state to toggle an element's class attribute on click events.

The `button` component implementes `IRender (render [_])` which takes a single argument; the reify instance.

You'll need to implement `IRenderState (render-state [_ state])` which takes a second argument; a map of the component's current state.

> Other than the second argument, the two render protocols are identical. You should only implement one of them per component. Whichever you choose to implement will be called each time either the component or application state is changed.

Update the `button` and `hello-cp` components code to:

```clojure
(defn button [app owner]
  (reify
    om/IInitState
    (init-state [_]
      {:sizes ["14px" "28px"]})
    om/IRenderState
    (render-state [_ {:keys [sizes]}]
      (dom/button #js {:style #js {:font-size (first sizes)}
                       :onClick #(om/set-state! owner :sizes (reverse sizes))}
                  "Click Me to Change Size"))))


(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/span nil
                (dom/h1 nil "Hello World!")
                (om/build button app)))))

```

We've implemented `om/IInitState (init-state [_])`, which is called only once per Component. It must return a map with the desired initial Component state.

When the button is clicked, the values in the vector of `:colors` in the Component state map will be reversed. `om/set-state! takes the backing Om component, a key or seq of keys, and the new value to set.

Om will detect this state change, and the Component will be re-rendered. `render-state` will take the new state map, destructure it, and update the button element class attribute with the alternate class.


