**Elm 0.??**, **please ignore** 

# Elm Application Framework, Cheat Sheet

## Table of Contents

2. [Hello World](#hello-world)
14. [Ports](#ports)


## Hello World

File `HelloWorld.elm`:
```elm
import Html exposing (h1, text)
import Html.Attributes exposing (id)

-- Hello world example
main =
  h1 [id "hw"] [text "Hello World!"]
```

