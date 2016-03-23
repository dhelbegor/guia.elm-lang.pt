# Radio Buttons

```elm
import Html exposing (Html, Attribute, text, toElement, div, input)
import Html.App as Html
import Html.Attributes exposing (..)
import Html.Events exposing (onInput)
import String


main =
  Html.simpleProgram { model = model, view = view, update = update }


-- MODEL

type alias Model =
  { style : Style
  }

type Style
  = Red
  | Underline
  | Bold

model =
  { style = Bold }


-- UPDATE

type Msg =
  Switch Style

update : Msg -> Model -> Model
update (Switch newStyle) model =
  { model | style = newStyle }


-- VIEW

view : Model -> Html Msg
view model =
  div []
    [ span [toStyle model] [text "Hello, how are you?!"]
    , radio Red "red" model
    , radio Underline "underline" model
    , radio Bold "bold" model
    ]

toStyle : Model -> Attribute msg
toStyle model =
  style <|
    case model.style of
      Red ->
        [ ("color", "red") ]

      Underline ->
        [ ("text-decoration", "underline") ]

      Bold ->
        [ ("font-weight", "bold") ]

radio : Style -> String -> Model -> Html Msg
radio address model style name =
  let
    isSelected =
      model.style == style
  in
    div []
      [ input [ type' "radio", checked isSelected, onCheck (\_ -> style) ] []
      , text name
      ]
```