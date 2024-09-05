HUD Menus ====

Before working on HUD, it\'s recommended to
[extract](https://noskill.gitbook.io/titanfall2/intro/duction/vpk-packpack)
the `englishclient_frontend.bsp.pak000_dir.vpk` vpk. This file contains
all vanilla menus and UI logic and will be a very helpful reference!

Registering a menu \-\-\--

In your `mod.json`, add a `Before` UI callback like this:

``` 
{
    "Path": "ui/profiles_menu.nut",
    "RunOn": "UI",
    "UICallback": {
        "Before": "InitProfilesMenu",
    }
}
```

In the script you referenced, create a global in which you register your
menu with the `AddMenu` like this:

``` 
global function InitProfilesMenu

void function InitProfilesMenu()
{
    AddMenu( "MenuName", $"path/to/menu.menu"  )
}
```

If you want to, you can add a init to `AddMenu` like this:
`AddMenu( "MenuName", $"path/to/menu.menu", func )`

The returns `void` and takes no parameters. It gets called once the menu
is initialized.

It\'s recommended to create a file struct in which you store menu
states:

``` 
struct {
    var menu
} file

void function MenuInitCallback()
{
    file.menu = GetMenu( "MenuName" )
}
```

Registering a Submenu \-\-\--

Menu Functions \^\^\^\^

Useless functions have been left out. From `_menus.nut`

Register Menus \~\~\~\~

> Register a normal HUD menu. The init function will be called once all
> menus are registered and created.

> Registers a normal HUD menu with a custom function to create the menu.
> The create function needs to be native since scripts can\'t create HUD
> elements.

Open Menus \~\~\~\~

> Push a menu to the stack / open a menu

> if `updateMenuPos` is not `null`, the menu is required to have a
> `ButtonFrame` element that is the main content reference.

Retrieve Menus \~\~\~\~

> Get the menu reference

Close Menus \~\~\~\~\~

> Close until the menu is the most recent opened.

Callbacks \~\~\~\~

> Accepted events:
>
> -   `eUIEvent.MENU_OPEN`
> -   `eUIEvent.MENU_CLOSE`
> -   `eUIEvent.MENU_SHOW`
> -   `eUIEvent.MENU_HIDE`
> -   `eUIEvent.MENU_NAVIGATE_BACK`
> -   `eUIEvent.MENU_TAB_CHANGED`
> -   `eUIEvent.MENU_ENTITLEMENTS_CHANGED`
> -   `eUIEvent.MENU_INPUT_MODE_CHANGED`

> Accepted events:
>
> -   `eUIEvent.PANEL_SHOW`
> -   `eUIEvent.PANEL_HIDE`

> Add an event handler to an element.
>
> If you have a reference to the element, use `Hud_AddEventHandler`

> Add a event handler for every element of a class

> Get the last openend menu that isn\'t a dialog

> Returns `true` if the menu is a dialog.

Submenus \~\~\~\~

Not recommended to use.

Other \~\~\~\~

> Debugging

> Set the default focus element to be focused

> Like `FocusDefaultMenuItem` but excludes some menus.

Footers \^\^\^\^

To use footers, add this element to your menu:

``` 
FooterButtons
{
    ControlName         CNestedPanel
    InheritProperties   FooterButtons
}
```

> Adds a footer to a menu.

> Adds a footer to a panel

> Update the footers of the active menu.

> Change the text of a specific footer.
