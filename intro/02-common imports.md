**Elm 0.??**, **please ignore** 

# Common imports

Here we list some of the libraries that get commonly imported in any typical front-end application. 

As Elm is a rapidly evolving language, the URLs provided may link to outdated versions, which should in turn link to newer versions.

## Keyboard 2.1.0

```elm
type alias KeyCode = Int
arrows : Signal { x : Int, y : Int }
wasd : Signal { x : Int, y : Int }
enter, space, ctrl, shift, alt, meta, isDown are all : Signal Bool
The meta key is the Windows key on Windows and the Command key on Mac.
keysDown : Signal (Set KeyCode) presses : Signal KeyCode
main= Signal.mapshowKeyboard.keysDown--showskeyCodesforcurrentlypressed keys
← 37, ↑ 38, → 39, ↓ 40
```

## Mouse 2.1.0

```elm
position : Signal (Int, Int)
x : Signal Int
x : Signal Int
isDown:SignalBool (State of the left mouse button; apparently no way to check the right mouse button.)
clicks:Signal() (Event triggers on every mouse click.) HTML
The syntax of an HTML tag is<tagattributes>Contents</tag>. In Elm this is represented as a function with two list arguments: tag [attributes] [Contents]. The attributes are of type Attribute, and there are assorted methods in Html.Attributesfor creating these.
The following types can be displayed: Element, Html, (Signal Element), (Signal Html). show : a -> Element
Converts any type of value to a displayable Element. Strings and characters are shown with enclosing quote marks.
text : String -> Svg.Svg
Turns a String into a graphical element that can be displayed. Html.ul [] [ li [] [ text "Hello" ], li [] [ text "there" ] ]
```