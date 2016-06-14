**Elm 0.??**, **please ignore** 

#  Commands and subscriptions

## COMMANDS (CMD)

- specifies what effect is needed
- and how to come back to the application (what messages)

```elm
update : Msg -> Model -> (Model, Cmd Msg)
update msg model =
  case msg of
    RequestMore ->
      ( model, getRandomGif model.topic )

    NewGif maybeUrl ->
      ( Model model.topic (Maybe.withDefault model.gifUrl maybeUrl)
      , Cmd.none
      )
```

(source: [elm-platform -- Upgrading to 0.17](https://github.com/elm-lang/elm-platform/blob/master/upgrade-docs/0.17.md))


## COMMMAND FROM TASK

    getSiiliOfficeCmd =
      Task.perform SiiliOfficeFailure SiiliOfficeSuccess getSiiliOffice

## TO PERFORM THE COMMAND:

```elm
main =
  Html.program
    { init = (initialModel, getSiiliOfficeCmd)
    , view = view
    , update = update
    , subscriptions = always Sub.none
    }
```


Or:

```elm
update msg model =
  case msg of
    ...
    GetSiiliOffice ->
      (model, getSiiliOfficeCmd)
    ...
```


##



Commands — A command is a way of demanding some effect. Maybe this is asking for a random number or making an HTTP request. Anything where you are asking for some value and the answer may be different depending on what is going on in the world.

Subscriptions — A subscription lets you register that you are interested in something. Maybe you want to hear about geolocation changes? Maybe you want to hear all the messages coming in on a web socket? Subscriptions let you sit passively and only get updates when they exist.

Together, commands and subscriptions make it possible for your Elm components to talk to the outside world. But how do these new concepts fit into what we already know?

(source: An introduction to Elm)


```elm
-- MODEL


type alias Model =
  { ...
  }


-- UPDATE

type Msg = Submit | ...

update : Msg -> Model -> (Model, Cmd Msg)
update msg model =
  ...


-- VIEW

view : Model -> Html Msg
view model =
  ...


-- SUBSCRIPTIONS

subscriptions : Model -> Sub Msg
subscriptions model =
  ...


-- INIT

init : (Model, Cmd Msg)
init =
  ...
```


(source: An introduction to Elm)

The update function now returns more than just a new model. It returns a new model and some commands you want to run. These commands are all going to produce Msg values that will get fed right back into our update function.

There is a subscriptions function. This function lets you declare any event sources you need to subscribe to given the current model. Just like with Html Msg and Cmd Msg, these subscriptions will produce Msg values that get fed right back into our update function.

So far init has just been the initial model. Now it produces both a model and some commands, just like the new update. This lets us provide a starting value and kick off any HTTP requests or whatever that are needed for initialization.

(source: An introduction to Elm)

## SUBSCRIPTIONS (SUB)

- for listening for external messages
- specifies how to prompt the application (what message)

SUB - EXAMPLE

```elm
main =
  Html.program
    { init = init
    , view = view
    , update = update
    , subscriptions = always (Geolocation.changes CurrentPlace)
    }
```
