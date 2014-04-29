# Seed a Root Component in the DOM

To build an app, being by seeding a root component.

You'll be able to branch from the root with more components.

![](http://www.luccidesigns.co.uk/assets/images/plant.jpg)

Use `root` to render the `hello-cp` component to the DOM.

```clojure
(om/root
  hello-cp {} {:target (. js/document (getElementById "app"))})
```

This establishes an Om rendering loop on the DOM element 
in index.html which has the property `id="app"`.

The rendering loop ensures that when when a state change occurs, 
our component will react and render the current state.
This component makes no use of state and will always render the same output:

> ```html
> <h1>Hello World!</h1>
> ```

