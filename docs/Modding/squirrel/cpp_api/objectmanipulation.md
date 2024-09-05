Creating / Manipulating Objects \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

# Arrays

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger size
>
> :   initial size of the array
>
> returns
>
> :   a `SQRESULT`
>
> creates a new array and pushes it to the stack
>
> ``` cpp
> newarray(sqvm, 0);
> pushstring(sqvm, "val1");
> arrayappend(sqvm, -2);
> pushinteger(sqvm, 15);
> arrayappend(sqvm, -2);
>
> /*
>     The array on the stack now looks like this:
>     [ "val1", 15 ]
> */
> ```


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the array to append to
>
> returns
>
> :   a `SQRESULT`
>
> pops a value from the stack and pushes it to the back of the array at
> the position idx in the stack

# Tables


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> returns
>
> :   a `SQRESULT`
>
> creates a new table and pushes it onto the stack.

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   the index of the table to insert into
>
> param SQBool bstatic
>
> :   if `SQTrue` creates a static member. This parameter is only used
>     if the target object is a class.
>
> pops a key and a value from the stack and performs a set operation on
> the table or class that is at position idx in the stack, if the slot
> does not exist it will be created.
>
> ``` cpp
> newtable(sqvm);
> // slot 1
> pushstring(sqvm, "key");
> pushstring(sqvm, "value");
> newslot(sqvm, -3);
> // slot 2
> pushstring(sqvm, "key2");
> pushasset(sqvm, "value2");
> newslot(sqvm, -3);
> // slot 3
> pushstring(sqvm, "key3");
> newtable(sqvm);
> pushstring(sqvm, "sub");
> pushinteger(sqvm, 13);
> newslot(sqvm, -3);
> newslot(sqvm, -3);
>
> /*
>     The table on the stack now looks like this:
>     {
>         key = "value"
>         key2 = $"value2"
>         key3 = { sub = 13 }
>     }
> */
> ```

# Structs

!!! note

These functions aren\'t available for plugins yet.
::::



> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param int fieldCount
>
> :   total number of fields the struct contains
>
> Creates and pushes a struct instance with `fieldCount` to the stack.

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param int fieldIndex
>
> :   Index of the field to fill
>
> Pops a value from the stack and fills the field at `fieldIndex` from
> the struct object that needs to be at the top of the stack.
>
> ``` cpp
> pushnewstructinstance(sqvm, 2); // create a struct instance with 2 slots
> pushinteger(sqvm, 12);
> sealstructslot(sqvm, 0);
> pushstring(sqvm, "example", -1);
> sealstructslot(sqvm, 1);
>
> /*
>     Assuming the compiler expects this slot:
>     struct ExStruct { int i, string s }
>     , the struct on the stack looks like this
>
>     ExStruct {
>         i = 12,
>         s = "example"
>     }
> */
> ```

# Userdata

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQInteger size
>
> :   bit size of the userdata object
>
> When the function sq_newuserdata is called, Squirrel allocates a new
> userdata with the specified size, returns a pointer to his payload
> buffer and push the object in the stack; at this point the application
> can do whatever it want with this memory chunk, the VM will
> automatically take care of the memory deallocation like for every
> other built-in type. A userdata can be passed to a function or stored
> in a table slot. By default Squirrel cannot manipulate directly
> userdata; however is possible to assign a delegate to it and define a
> behavior like it would be a table. Because the application would want
> to do something with the data stored in a userdata object when it get
> deleted, is possible to assign a callback that will be called by the
> VM just before deleting a certain userdata. This is done through the
> API call sq_setreleasehook.

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQInteger stackpos
>
> :   Stack position of the userdata

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQInteger stackpos
>
> :   Stack position of the userdata
>
> param T\* data
>
> :   Pointer to an arbitrary variable the userdata gets mapped to
>
> param uint64_t\* typeid
>
> :   Pointer to a variable edited to hold the userdata type
