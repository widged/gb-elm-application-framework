**Elm 0.??**, **please ignore** 

# Optimization

While Elm is fast [at some things](http://elm-lang.org/blog/blazing-fast-html), it's easy to write non-performant code in Elm if you stick too rigidly to the functional programming style.

(source: [elm-for-web-developers](https://github.com/eeue56/elm-for-web-developers))

## Move things out of let bindings

If a function can be defined outside of a let binding, then take it out. 

TODO: add example

(source: [elm-for-web-developers](https://github.com/eeue56/elm-for-web-developers))

## Flat is better than nested

The less levels of functions involved, the better. If you find yourself nesting function calls within function calls over and over, look and see if you can simplify.

(source: [elm-for-web-developers](https://github.com/eeue56/elm-for-web-developers))