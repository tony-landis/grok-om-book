# The App State Atom

Om app state is held in an [atom](http://clojure.org/atoms) and
passed as the second argument of `root`. 


![](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSMUpV_bD3qO7rBSHeFMz8Ln2gFjpmYYbLCeDU9yto5OHIR8d-F)

Components take the app state as their first argument.


```clojure
;              ↓ app state
(def app-state (atom {:text "Hello World from App State"}))

(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_] ;        ↓ app state
      (dom/h1 nil (:text app)))))

;                 ↓ app state
(om/root hello-cp app-state {:target (. js/document (getElementById "app"))})
```

> Om convention is to pass app state around as `app`.
