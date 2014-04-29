# Component Intercom

Communication between components takes place on 
[core.async](https://github.com/clojure/core.async/blob/master/examples/walkthrough.clj)
 channels. Update your namespace form:

```clojure
(ns grok-om.core
  (:require-macros [cljs.core.async.macros :refer [go]])
  (:require [om.core :as om :include-macros true]
            [om.dom :as dom :include-macros true]
            [cljs.core.async :refer [put! chan <!]]))
```

Let's refactor our button style toggler to use use a core.async channel:

```clojure
(defn button [app owner]
  (reify
    om/IRenderState
    (render-state [_ {:keys [event-ch]}]
      (dom/button #js {:style #js {:font-size (first (:sizes app))}
                       ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; 4
                       :onClick #(put! event-ch :click)}
                  (:text app)))))

(defn hello-cp [app owner]
  (reify
    om/IInitState
    (init-state [_]
      ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; 1
      {:event-ch (chan)}) 
    om/IWillMount
    (will-mount [_]
      ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; 2
      (let [event-ch (om/get-state owner :event-ch)]
        (go (loop []
              ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; 5
              (let [e (<! event-ch)]
                (when (= e :click)
                  (om/transact! app [:button :sizes] reverse)))
              (recur)))))
    om/IRenderState
    (render-state [_ {:keys [event-ch]}]
      (om/build button (:button app)
                ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;; 3
                {:init-state {:event-ch event-ch}}))))
```

Here is a walkthrough of the flow:

1. Allocate the core.async channel `event-ch` in the the root component's state.
2. Implement `IWillMount` and establish a go loop to listen for events from child components.
3. Pass the channel to the button component via `:init-state`.
4. Write event keyword `:event` onto the channel.
5. Read the event keyword from the channel and reverse the sizes in app state.

`IWillMount` runs once per component before rendering.



