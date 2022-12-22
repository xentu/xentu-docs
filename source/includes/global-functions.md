# Global Functions

There are some functions that Xentu needs to provide, and make accessible 
anywhere in your code. So in this section we will go over what they are.

Some functions have already been explained above in the custom events section, 
so they will be omitted here.

## game.exit()

```javascript
game.exit();
```
```lua
game.exit()
```
```python
game.exit()
```

Calling this function immediately closes the game, cleaning up used resources
before hand.

## include(path)

```javascript
include("/includes/other.js");
```
```lua
include("/includes/other.lua")

-- can also load compiled lua files.
include("/includes/other.luac")
```
```python
include("/includes/other.py")
```

The include function uses the virtual file system to load code from another code
file, and then executes it within the current context. This is very useful for
splitting your game code into smaller organised files.

It's common to confuse this with the native exec() function. The differences
depend on language, but the main one is that include() is provided by the engine,
while exec() does not use the VFS, and adheres to rules found in the language. 
For example JavaScript will usually give code ran in exec() it's own context, 
while include() wont. Exec will usually always returns a result also.

These differences are important to be aware of, as there are valid situations
where you may need to use both.

## print(args...)

```javascript
print("Hello World");
```
```lua
print("Hello World")
```
```python
print("Hello World")
```

The print global function handles printing information to the console window 
when debugging. Xentu typically provides binaries in two flavours, with one 
being for debugging.

For example in Windows, xentu ships as `xentu.exe` and `xentu_debug.exe`. If you
use the `print()` function with the binary ending with _debug in the name, your
text will output, while using the non debug will hide it.

