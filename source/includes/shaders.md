# Shaders

Most of the time you probably wont need to interfere with custom shaders. But if
you decide to use them, having the ability to communicate info with them
can become very important.

This section goes over how to send information to shaders. It's important to 
recognise that whilst the methods here are for interacting with GLSL (OpenGL 
shader language), when DirectX (HLSL) and other API support comes along, these 
will work for those as well.

## shader.get_location

```javascript
const var_loc = shader.get_location("my_variable");
```
```lua
var_loc = shader.get_location("my_variable")
```
```python
var_loc = shader.get_location("my_variable")
```

<code class="definition"><b>int</b> result = shaders.get_location(<b>string</b> variable_name)</code>

Gets the location id for a variable within the currently loaded shader. You need
to call this if you are to use the methods below.

## shader.set_bool

```javascript
shader.set_bool(var_loc, true);
```
```lua
shader.set_bool(var_loc, true)
```
```python
shader.set_bool(var_loc, true)
```

<code class="definition">shaders.set_bool(<b>int</b> location, <b>bool</b> value)</code>

Send a boolean value to a variable on the currently loaded shader.

## shader.set_int

```javascript
shader.set_int(var_loc, 5);
```
```lua
shader.set_int(var_loc, 5)
```
```python
shader.set_int(var_loc, 5)
```

<code class="definition">shaders.set_int(<b>int</b> location, <b>int</b> value)</code>

Send an integer value to a variable on the currently loaded shader.

## shader.set_float

```javascript
shader.set_float(var_loc, 2.0);
```
```lua
shader.set_float(var_loc, 2.0)
```
```python
shader.set_float(var_loc, 2.0)
```

<code class="definition">shaders.set_float(<b>int</b> location, <b>float</b> value)</code>

Send a float value to a variable on the currently loaded shader.