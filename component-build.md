# Build Options

`build` takes an optional map as its third argument, several of which relate to application state. For now we'll discuss only the ones unrelated to application state.

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQYNg66hyNwnjppzf3J0EUBypMSVjTMD2aGLgyrwZw8Idm2QHBDKA)


## `:init-state` Provides Initial Component State

Use this key to pass a map which will be merged into the map returned by `IInitState`. Any keys returned by `IInitState` will override the same keys present in `:init-state`.

```clojure
(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/span nil
                (dom/h1 nil "Hello World!")
                (om/build button app {:init-state {:sizes ["5px" "10px"]}})))))
```



## `:opts` Provides Component Opts

Use this key to pass a map of side information that is unrelated to either application or component state. It will be passed as the third argument the component.

```clojure
(defn a-component [_ _ opts] ...)

(om/build a-component app {:opts {:some "value"}})
```
