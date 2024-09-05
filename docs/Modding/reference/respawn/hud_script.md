# HUD elements in Scripts

Script methods to manipulate hud elements.

## Element Tree & Locating Elements

> Returns a reference to the menu the passed element is parented to

> Returns the next higher parent of the element

> Returns `true` if the element has a child named like `childName`

> Returns the child element of the passed element named like `childName`

> Returns all children that have the given class

> Returns the script ID of the element declared in the .menu file

> Returns the currently focused element.

### Element Position

> Set the position of the element **relative** to the base position.

> Returns an array of type `int[2]` as a `var`. The position is
> **relative** to the element\'s base position.

> Only change the x position relative to the base position.

> Only change the y position relative to the base position.

> Returns the x position of the element relative to it\'s base position.

> Returns the y position of the element relative to it\'s base position.

> Set the position of this element to it\'s base position.

> Returns an orray of type `int[2]` as a `var`. Base position is always
> `[0,0]`

> Returns the base x of this element.

> Returns the base y of this element.

> Returns an array of type `int[2]` as a `var`. Absolute coordinates on
> the screen of this element.

> Returns the absolute x position on the screen of this element.

> Returns the absolute y position of the screen of this element.

> Move to relative x over time with interpolation.
>
> -   `INTERPOLATOR_LINEAR`: linear interpolation
> -   `INTERPOLATOR_ACCEL`: move with accelerating speed
> -   `INTERPOLATOR_DEACCEL`: move with deaccelerating speed
> -   `INTERPOLATOR_PULSE`: one time bounce
> -   `INTERPOLATOR_FLICKER`: no transition
> -   `INTERPOLATOR_SIMPLESPLINE`: ease in / out
> -   `INTERPOLATOR_BOUNCE`: gravitational bounce

> Move to relative y over time with interpolation

> Returns the angles of the element

> Set the angles of the element

## Visibility & Color

> Make this element visible

> Make this element invisible

> Returns `true` if the element is visible

> Set if the element is visible

> Set the color of the element

> Change the color of the element over time

> Change the color of the element over time

> Change the opacity of the element

> Change the opacity of the element over time

> Change the opacity of the element over time after a delay

## Element Dimensions

> Returns the current width of the element.

> Set the width of an element.

> Returns the width an element got initialized with.

> Returns the current height of an element.

> Set the heigth of an element.

> Returns the heigth an element got initialized with.

> Returns an array of type `int[2]` as a `var`. The first index is width
> and the second height of the element.

> Set width and height of the element.

> Returns the width and height values the element got initialized with
> as an array of type `int[2]` as `var`.

> Set the width and height of the element over time.
>
> The final width and height is calculated like this:
> `width * width_factor`

> Set the width of the element calculated with a factor.

> Set the height of the element calculated with a factor.

> Return to base width and height

## Text

> Set the text content of this element

> Returns the current text of the element. Useful for text inputs

> Set the text of an rui, if the element contains an rui that takes
> string input.

## Element Status

> Returns `true` if the element is locked.
>
> Locked elements are visible, can be focused and selected but don\'t
> trigger events and play a locked sound if they are selected

> Set this element locked status

> Returns `true` if the element is enabled
>
> Disabled elements are visible but can\'t be focused or selected and
> don\'t trigger events.

> Set this element to be enabled / disabled

> Returns `true` if this element is focused
>
> Focused elements will be selected when pressing enter

> Set the element to be focused

> Returns `true` if this element is selected

> Set this element to be selected / not unselected

> Select this element and all children

> Returns `true` if the element is a label

## Element RUI

> Returns `true` if this element can contain ruis

> Returns the rui instance of this element.

## Navigation

> Set the element that will be selected when navigating up (arrow up)
> from this selected element.

> Set the element that will be selected when navigating up (arrow up)
> from this selected element.

> Set the element that will be selected when navigating left (arrow
> left) from this selected element.

> Set the element that will be selected when navigating right (arrow
> right) from this selected element.

## Events

> Fire the specified event for the element

> Handle an event for the element
>
> Accepted events:
>
> -   `UIE_CLICK`
> -   `UIE_GET_FOCUS`
> -   `UIE_LOSE_FOCUS`
> -   `UIE_CHANGE`

## Other Visuals

> Set the image displayed by the element, if the elements controlName
> allows for it.

## Slider

## Graphs

## Client Settings

## Uncategorized
