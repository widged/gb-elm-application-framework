**Elm 0.??**, **please ignore** 

## HTML Embedding
Running fullscreen
`elm-make HelloWorld.elm` -> `elm.js`
```html
<script type="text/javascript" src="elm.js"></script>
<script type="text/javascript">
    Elm.fullscreen(Elm.HelloWorld);
</script>
```

Embed explicitly in a html element
```html
<script type="text/javascript" src="elm.js"></script>
<script type="text/javascript">
    var elmHolder = document.getElementById('hw-wrapper');

    Elm.embed(Elm.HelloWorld, elmHolder);
</script>
```

Run without graphics
```javascript
Elm.worker(Elm.HelloWorld);
```
(source: [learnyouanelm](https://github.com/learnyouanelm/learnyouanelm.github.io/blob/master/pages/02-starting-out.md))


# Integrating Elm into your existing applications

`Elm.worker(Elm.ModuleName)` should be your best friend for integrating Elm into existing applications. It allows you to use ports and use Elm for controlling your applications without needing to have any of the views in Elm itself. I've used it for managing state in my React apps between the different components. The `send` function allows your child components to trigger `subscribe` functions in your parent scope, keeping your data flow in a top-down structure as promoted by things like Flux.

`Elm.embed(Elm.ModuleName)` is perfect for when you want to do some of your view in Elm, but the rest without. Note: there are some bugs with the core libraries when you use embed, for things like `touch` or `mouse` actions.

With either of these, you can use ports for allowing communication between your Javascript and your Elm applications. A typical use case of this might be using existing AJAX requests without moving all the HTTP requests to Elm.

(source: [elm-for-web-developers](https://github.com/eeue56/elm-for-web-developers))

# Links

[Sending messages to sibling components in Elm Architecture](https://github.com/sporto/elm-arch-siblings)
