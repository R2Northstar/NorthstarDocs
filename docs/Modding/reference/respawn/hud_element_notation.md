Elements are notated as
[VDF](https://developer.valvesoftware.com/wiki/KeyValues)

UI elements are created when a menu is initialized. References to the
elements will stay the same, regardless if the menu is open or not.

It is not possible to create elements at runtime so you have to define
all elements a menu or panel contains beforehand in appropriate files.

An Element is declared in the following way:

``` 
// please follow this structure
ElementName
{
    ControlName name
    // optional: classname, inheritance, ids ...

    // optional: other properties

    // optional: pinning
}
```

If you\'re working on a **menu**, you need a `menu` object that contains
all elements, for example like this:

``` 
resource/ui/menus/profiles_menu.menu
{
    menu
    {
        ControlName Frame
        xpos 0
        ypos 0
        zpos 3
        wide f0
        tall f0
        autoResize 0
        visible 1
        enabled 1
        pinCorner 0
        PaintBackgroundType 0
        infocus_bgcolor_override "0 0 0 0"
        outoffocus_bgcolor_override "0 0 0 0"

        // elements
    }
}
```

It usually doesn\'t matter if you use quotation marks to assign string
values to parameters.

# HUD & Panel files

The first line of a `.menu` or `.res` file needs to be the resource path
to itself, starting from the resource folder.

It\'s not possible to load other files as menus or panels. A `.menu`
represents an independant menu of the game, while `.res` files are
\"Panels\" that can be loaded from other elements.

The rest of the file needs to be wrapped in curly brackets.

``` 
resource/ui/menus/more/folders/my_menu.menu
{
    MyObject
    {
        // object properties go here
    }

    // more objects ...
}
```

## Properties

Capitalization of the properties shouldn\'t matter.

> This isn\'t a regular property and comes **before** the opening
> bracket
>
> Unique string identifier used in scripts to look up an element. Every
> element is required to have a name.

### Inheritance / Parenting

> Controls what type of Component the element is and what parameters
> have an effect. Every element is required to have control name.

> Load a `.res` file. All elements in the settings file are instantiated
> and set as children of the element.
>
> `Hud_GetChild` only works if the parent element is (has the
> `ControlName`) a **CNestedPanel**!

### Identifying

> Classname used for identifying groups of elements

> Set an unique integer id for this element that\'s retrievable in
> script.

### Position

> Set the base x position relative to the element\'s sibling position.
>
> inverted when attached to the left corner or smth

> Set the base y position relative to the element\'s sibling position.
>
> inverted when attached to the top corner or smth

> The layer this element sits in. Elements with a higher z will be
> prioritized to be selected / focused. They are also drawn on top of
> elements with a lower z position.

Dimensions \^\^\^\^

> Set the base width of this element.

> Set the base height of this element.

> Float that scales the element.

### Text

> Set the label text of this element, if it is a Label.

> Controls the element boundary point the element\'s text gets aligned
> with. `east` -\> Left, `north` -\> Top, `west` -\> Right, `south`
> Bottom.
>
> You can also combine the directions like this: `north-west`.

> Controls if the text of this element is rendered in all caps. Defaults
> to 0.

> Set the text font of this element.

> don\'t wrape text

> wrap text from east

> wrap text from center

> Set if the text input supports multiline input.

Pinning \^\^\^\^

> Controls the sibling this element will be pinned to. Takes an
> element\'s name as a parameter.

> Sets which corner of this element is pinned to the sibling.

> Set to which corner of the sibling this element is pinned to.

### Rui

Images \^\^\^\^

> vgui asset to render

> apply this color on top. Format is \"r g b a\".

> Fill transparent pixels with this color. Format is \"r g b a\"

Navigation \^\^\^\^

Slider \^\^\^\^

Other \^\^\^\^

> Controls if this element is rendered. Defaults to 1.

> Controls if this element starts enabled. Defaults to 1.

> Controls if this element is enabled. Only enabled elements can be
> focused / selected. Defaults to 1.

> // 0 for normal(opaque), 1 for single texture from Texture1, and 2 for
> rounded box w/ four corner textures

Conditional Properties \~\~\~\~

You can declare properties for specific conditions by adding
`[CONDITION]` after the property value.

When putting a condition after an element\'s name, the element will only
be created if the condition evaluates to true.

Usable conditions are:

> game is running on 32 bit windows

> game is running on windows

> game is running on xbox

> game is running on a PS4

> game resolution is 16/9

> the game\'s language.
>
> ``` text
> // use allcaps only in russian
> allCaps                 0   [!$RUSSIAN]
> allCaps                 1   [$RUSSIAN]
> ```

On top of that, logical operators like `!`, `&&` and `||` are available
as well.

Example: \^\^\^\^

``` text
// This element only shows on pc
IngameTextChat [$WINDOWS]
{
    ControlName             CBaseHudChat
    InheritProperties       ChatBox

    destination             "match"

    visible                 0

    pin_to_sibling          Screen
    pin_corner_to_sibling   TOP_LEFT
    pin_to_sibling_corner   TOP_LEFT
    xpos                    -45
    ypos                    -616
}

// This element has different widths depending on the game resolution
LoadingTip
{
    ControlName             Label
    ypos                    10
    wide                    1630 [$WIDESCREEN_16_9]
    wide                    1441 [!$WIDESCREEN_16_9]
    auto_tall_tocontents    1
    labelText               ""
    textalign               "north-west"
    font                    Default_28
    wrap                    1
    fgcolor_override        "217 170 75 255"
    visible                 0

    pin_to_sibling          LoadingGameMode
    pin_corner_to_sibling   TOP_LEFT
    pin_to_sibling_corner   BOTTOM_LEFT
}
```

Pinning \~\~\~\~

> The calculated center of the element

> Element\'s top y bounds, x axis center.

> Element\'s lowest y bounds, x axis center.

> Element\'s lowest x bounds, y axis center.

> Element\'s highest x bounds, y axis center.

> Top left corner

> Top right corner

> Bottom left corner

> Bottom right corner

Units \~\~\~\~

You can calculate the position or dimensions etc. with different units.
If you provide no extra unit, the game uses pixels.

> x percent of the screen.
>
> > // cover the entire screen width %100 height %100

> use 100%

> something with the screen edges not exactly sure how positions get
> calculated

Including KeyValues \~\~\~\~

To include another KeyValue file, use `#base "filepath"` at the top of a
VDF file.
