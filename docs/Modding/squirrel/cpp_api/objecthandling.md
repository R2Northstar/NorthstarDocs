!!! warning


Parameters or descriptions may be wrong or incomplete

This list is incomplete and only lists methods available in
[squirrel.h](https://github.com/R2Northstar/NorthstarLauncher/blob/main/NorthstarDLL/squirrel/squirrel.h).

Some descriptions are taken from the [Squirrel
Documentation](http://www.squirrel-lang.org/mainsite/squirreldoc/reference/api_reference.html)
::::

# Object creation and handling

> You can access all sq functions only with a `SquirrelManager`
> instance. You have one available inside the `ADD_SQFUNC` macro.

## Pushing Objects to the stack


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQInteger bVal
>
> :   the bool that will be pushed
>
> pushes a boolean to the stack


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQInteger iVal
>
> :   the integer that will be pushed
>
> pushes an integer to the stack


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQInteger fVal
>
> :   the float that will be pushed
>
> pushes a float to the stack

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQChar\* sVal
>
> :   the string that will be pushed
>
> param int len
>
> :   length of the string `sVal`
>
> remarks
>
> :   if the parameter length is less than 0 the VM will calculate the
>     length using `strlen`
>
> pushes a string to the stack

# pushasset

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQChar\* sVal
>
> :   the string that will be pushed
>
> param int len
>
> :   length of the string `sVal`
>
> remarks
>
> :   if the parameter length is less than 0 the VM will calculate the
>     length using `strlen`
>
> pushes an asset to the stack

# pushvector


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param Vector3 vVal
>
> :   the vector that will be pushed
>
> pushes a vector to the stack

# pushobject


> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> param SQObject obj
>
> :   the object that will be pushed
>
> pushes an object like functions to the stack

# pushroottable

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target VM
>
> pushes the current root table into the stack

!!! note

`sq_pushnull` (`0x33D0`) and more aren\'t included in `squirrel.h` right
now but may be in the future.
::::

## Getting Objects from the stack

# getbool

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getinteger

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getfloat

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getstring

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getvector

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getasset}

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   The value of the object

# getConstants

> !!! note
>
> This function (`server.dll+0x5920`\`) is not available in the launcher
> or plugins at the moment.
>
> You can open a PR if you need it now.
>
> To define an integer constant you can use
> `defconst <defconst>`
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> returns
>
> :   the table of constants
>
> Pushes the constants table to the stack.
>
> Used to add global constants for scripts.
>
> ``` cpp
> getConstants(sqvm);
>
> pushstring(sqvm, "MY_CONSTANT");
> pushstring(sqvm, "MY_VALUE");
> newslot(sqvm, -3, false);
>
> removeFromStack(sqvm); // don't forget this!
> ```

# sq-getfunction

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQChar\* name
>
> :   the function name to search for
>
> param SQObject\* returnObj
>
> :   reference to the object to hold the function object
>
> param SQChar\* signature
>
> :   
>
> returns `0` if the function was found.
>
> ``` cpp
> SQObject functionobj {};
> int result = sq_getfunction(m_pSQVM->sqvm, funcname, &functionobj, 0);
> if (result != 0) // This func returns 0 on success for some reason
> {
>     NS::log::squirrel_logger<context>()->error("Call was unable to find function with name '{}'. Is it global?", funcname);
>     return SQRESULT_ERROR;
> }
> ```

# getentity

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQInteger iStackPos
>
> :   Stack position of the entity

# sq-getentityfrominstance

> 
>
> param CSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQObject\* pInstance
>
> :   Instance holding an entity
>
> param char\*\* ppEntityConstant
>
> :   Entity constant like
>     `__sq_GetEntityConstant_CBaseEntity <sq-GetEntityConstant-CBaseEntity>`

# sq-GetEntityConstant-CBaseEntity

> There are entity constants for other types, but seemingly
> CBaseEntity\'s is the only one needed

# sq-getobject

> 
>
> param HSquirrelVM\* sqvm
>
> :   The target vm
>
> param SQInteger iStackPos
>
> :   Stack position of the object
>
> param SQObject\* obj
>
> :   Pointer that will hold the object
>
> `obj` will be overwritten to hold the squirrel object.
>
> This example adds a native function with the
> `ADD_SQFUNC <sq-api-register-native-functions-c-macro>` macro. The function takes a function reference as a
> callback and calls it immediately. More information about function
> calls are available
> `here <sq-api-calling-functions>` 
>
> ``` cpp
> ADD_SQFUNC("void", SQCallbackTest, "void functionref()", "", ScriptContext::UI)
> {
>     SQObject fn; // Make an empty sqobject. This will hold the function object later
>     g_pSquirrel<context>->__sq_getobject(sqvm, 1, &fn); // Assign the function object to the SQOBJECT
>     g_pSquirrel<context>->pushobject(sqvm, &fn); // Push the function object for the call
>     g_pSquirrel<context>->pushroottable(sqvm); // Push the root table for the function stack
>     g_pSquirrel<context>->__sq_call(sqvm, 1, false, true); // call the function with one parameter (the 'this' object)
>
>     return SQRESULT_NULL;
> }
> ```

# get
> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param SQInteger stackpos
>
> :   stack position of the object
>
> returns
>
> :   an `SQRESULT` that indicates whether or not the access was
>     successful.
>
> pops a key from the stack and performs a get operation on the object
> at the position idx in the stack; and pushes the result in the stack.

## Stack Infos

## sq-stackinfos
> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param int level
>
> :   stack depth of the info
>
> param SQStackInfos& out
>
> :   instance that will hold the information

# getcallingmod

> 
>
> param HSquirrelVM\* sqvm
>
> :   the target vm
>
> param int depth
>
> :   stack depth of the origin mod
>
> returns
>
> :   Pointer to the Mod object at the stack depth
>
> !!! note
>
> Not available in
> [plugins](https://github.com/R2Northstar/NorthstarLauncher/blob/main/NorthstarDLL/plugins/plugin_abi.h)
> ::::

## Other

defconst

> 
>
> param CSquirrelVM\* csqvm
>
> :   the target vm
>
> param SQChar\* pName
>
> :   the constant name
>
> param int nValue
>
> :   the constant value
>
> defines a global squirrel integer constant
