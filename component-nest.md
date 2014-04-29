# Building Branches

A component will `build` other components, creating a branching
structure from the root component and up.

Every component takes the instance of the component from where it 
was called as its second argument. 

> Om convention refers to this calling instance as `owner`.
> I like to think of the owner "holding up" the components it calls.

![](http://www.landscapemodeling.org/html/ch3/images/small/sm3.31d.png)


To nest one component in another, `build`. 
Create the `button` component and update the `hello-cp` component:

```clojure
(defn button [app owner]
  (reify
    om/IRender
    (render-state [_]
      (dom/button nil "Click Me"))))

(defn hello-cp [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/span nil
        (dom/h1 nil "Hello World!")
        (om/build button app)))))
```

This will render a single button component after the h1 element.

---

To nest many of the same component, use `build-all`. 
Change the `(om/build ...)` form in `hello-cp` to:

```clojure
         (apply dom/div nil
                (om/build-all button [{} {}]))))))
```

This will render two button components after the h1 element.

