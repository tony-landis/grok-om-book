# Transactions to App State

Udating app state is done with `transact!` and `update!`.

Both take a cursor, and a location within that cursor.

`transact!` is analagous to `reset!` for atoms, and
`update!` is analogous to `swap!`.

```clojure
(transact! cursor :key-in-cursor fn)
(update! cursor :key-in-cursor val)
```


Let's refactor our button style toggler to use app state instead of component state.

```clojure
(def app-state (atom {:button {:text "Click Me"
                               :sizes ["14px" "28px"]}}))

(defn button [app owner]
  (reify
    om/IRender
    (render [_]
      (dom/button #js {:style #js {:font-size (first (:sizes app))}
                       :onClick #(om/transact! app [:sizes] reverse)}
                  (:text app)))))
```

Where `transact!` takes a fn which will operate on the current state as
its third argument, `update!` expects a new value.

The following form produces the same result as `#(transact! ...)` above:

```clojure
  #(om/update! app [:sizes] (reverse @sizes))}
```

Note that when using `update!`, if you forget to deref `sizes` using `@` you'll get this error:

> ``` Uncaught Error: Cannot manipulate cursor outside of render phase, ```
> ``` only om.core/transact!, om.core/update!, and cljs.core/deref operations allowed ```

> The problem is that we put a cursor directly onto a core.async channel.
> Cursors are only consistent during the application render phase - that is inside the life cycle methods.
> Callbacks on events handlers and core.async loops are not really a part of the Om/React render loop. 
> Thus you are not allowed to use cursors outside of the render phase as this is almost certainly a concurrency bug!
> Outside of the render phase you are only allowed to do two kinds of operations on cursors.
> You may use them to transition the application state or you can dereference them to get at their current value.

For this reason, it may be simpler to use `transact!` as the fn you provide
has already beed dereferenced.
