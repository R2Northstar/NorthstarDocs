# Safe I/O

If you want to store an extended amount of data in your mod it is not
sustainable to only use ConVars as they are limited in space and easily
reset. With Safe I/O you are able to write to one folder
(`<profile>/saves/<mod directory name>`). In this folder you can store
text files of any type (e.g. `.txt`, `.json`), it\'s also possible to
use non text file formats (e.g. `.exe`) however you won\'t be able to
run them on your PC. It also allows for sub-folders.

## Saving a file

To save a file you need the content you want to save as
`strings-overview`  , for this the
`json_overview`  functions can be useful if
you want to store `table_overview`  or
`arrays_overview` .

To actually save the file you use:

> 
>
> param string file
>
> :   The name of the file you want to store, this supports sub folders.
>     Needs to be with the file type (e.g. `/TitanData/tone.txt`).
>
> param string data
>
> :   The saved data, this can be any valid String.

Alternatively if you want a faster way to store
`table_overview`  you can use:

> 
>
> param string file
>
> :   The name of the file you want to store, this supports sub folders.
>     Doesn\'t have to be `.json` but will use the correct formatting
>     for a `.json`.
>
> param table data
>
> :   The table that will be written to the file, this only supports the
>     types specified in the `json_overview`.

## Loading a file

> 
>
> param string file
>
> :   This is the name of the file you want to load, it has the same
>     formating as in `NSSaveFile`.
>
> param void functionref( string ) onSuccess
>
> :   The function that gets execued when the file is successfully
>     loaded, the parameter `string` is the content of the loaded file.
>
> param void functionref() onFailure = null
>
> :   The function that gets execued when the loading was NOT
>     successful, by default the function is just `null`.
>
> !!! note
> !!! title
> Note
> :::
>
> If you are having trouble with functionrefs you can read up on them
> here: `functionref_overview` 
> ::::

You can also get all saved file:

> 
>
> param string path = \"\"
>
> :   Gets all files in a specified path, by default its just
>     `<profile>/saves/<mod directory name>`.
>
> returns
>
> :   An array with all file names in the specified path.

## Deleting a file

> 
>
> param string file
>
> :   This is the name of the file you want to check exsits, it has the
>     same formating as in `NSSaveFile`.

## File checks

> 
>
> param tring file
>
> :   This is the name of the file you want to check exsits, it has the
>     same formating as in `NSSaveFile`.
>
> returns
>
> :   `true` if the file was found, otherwise it returns `false`.

> 
>
> param string file
>
> :   This is the name of the file you want to get the file size from.
>
> returns
>
> :   KB size of the specified file.
>
> !!! warning
> !!! title
> Warning
> :::
>
> This fucntion will raise an error when the file doesnt exist.
> ::::

> 
>
> param string file
>
> :   This is the path you want to check.
>
> returns
>
> :   `true` if the path is a folder, otherwise it returns `false`.

> 
>
> returns
>
> :   Amount of KB you have left to write on.
>
> !!! note
> !!! title
> Note
> :::
>
> The max size of data you can store is `50MB` per mod. Can be
> overwritten with `-maxfoldersize BYTES` in the launch args.
> ::::
