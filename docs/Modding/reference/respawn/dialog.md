# Dialogs

Dialogs are a way for a client to open a text window with up to 4
buttons.

## Dialog structs

All the data in the struct that can be changed.

> 

> 

> 

## Functions

> Shows the local player the dialog with the data from the struct.
>
> param DialogData dialog
>
> :   Instance of a DialogData struct
>
> **Example**
>
> ``` 
> DialogData dialog
> dialog.message = "Hello there"
> OpenDialog( dialog )
> ```

> Add one button to the given struct
>
> param DialogData dialog
>
> :   Instance of a DialogData struct
>
> param string text
>
> :   The Text that is shown on the button, supports some assets with
>     `%ASSET PATH%`
>
> param void functionref() callback
>
> :   Function that is executed when the button is pressed.
>
> **Example**
>
> ``` 
> void function SendDialogWithButton()
> {
>     DialogData dialog
>     dialog.message = "Hello there"
>     AddDialogButton(dialog, "Button 1 %%$r2_ui/menus/loadout_icons/primary_weapon/primary_kraber%%", void function():() {
>         printt( "pressed button 1" )
>     })
>     OpenDialog( dialog )
> }
> ```

> Adds a footer to the dialog struct
>
> param DialogData dialog
>
> :   Instance of a DialogData struct
>
> param string text
>
> :   The Text that is shown on the button, supports some assets with
>     `%ASSET PATH%`

> 
>
> param DialogData dialog
>
> :   Instance of a DialogData struct
>
> returns
>
> :   `true` if the dialog with that struct is currently open, otherwise
>     it returns `false`

> 
>
> param string errorDetails
>
> :   User facing information about the error

## Code example

the folowing code produces this output:

``` 
DialogData dialog
dialog.header = "This is the header"
dialog.message = "this is the body, it is green \n \n Hello There \n \n General Kenobi"
dialog.messageColor = [0,200,0,100]
dialog.showSpinner = true
dialog.showPCBackButton = true
AddDialogButton( dialog, "Button 1 %%$r2_ui/menus/loadout_icons/primary_weapon/primary_kraber%%", ButtonOnePressed )
OpenDialog( dialog )
```

<figure class="screenshotalign-center">
<img src="/_static/serverdialog/dialogexample.png" class="screenshot"
alt="/_static/serverdialog/dialogexample.png" />
</figure>
