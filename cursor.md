# Cursor, Where in the App am I!?

Components will be arbitrarily nested within apps. 
To preserve component modularity, a build-time address-to-state 
mechanism is needed.

A component's **cursors** points the component to
 the location of its data within app state.

![](http://media-cache-ec0.pinimg.com/236x/3b/76/cd/3b76cda7b9ca8fa32bf2582673f0f349.jpg)


Developers pass the app state atom `app` down 
the component assembly line and give each component their 
address within that atom. 

This enables addressing to happen when the component is called
with `build` or `build-all`
rather than when it is actually defined. 


```clojure
(def app-state (atom {:button {:text "Click Me"}}))

;              this component's cursor
;              ↓ into app-state
(defn button [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/button nil (:text app)))))

(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_] ;      ↓ cursor
      (om/build button (:button app)))))

(om/root hello-cp app-state {:target (. js/document (getElementById "app"))})
``` 

The `:fn` key in the opts map passed to `build` and `build-all` 
is an alternative way to specify a cursor location. 

Pass a function to apply on app state `app` before invoking the component:

```clojure
; keywords are functions in clojure/script:
(om/build button app {:fn :button})

; another way to do the same thing:
(om/build button app {:fn #(get % :button)})
```



![Curser](http://laughingsquid.com/wp-content/uploads/the-curser-20100126-154508.jpg)
