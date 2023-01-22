# Renderer

The renderer is responsible for drawing graphics onto the screen as fast as 
possible. To do this, it employs a technique called batch rendering, which 
groups draw calls by texture, vastly reducing how many instructions have to 
be sent to the GPU.

Batch rendering can be problematic for drawing layers on top of one another,
so the renderer provides a a way of simulating layers by providing `begin()`
and `present()` methods, which can be chained in pairs to get the desired
effect.

The batches drawn by game code are drawn onto the active render target, which
is usually the built in fixed size canvas, which then gets drawn onto the 
screen. This final step allows Xentu to place or scale the canvas on a window 
based on the viewport mode you specify in your configuration.

## clear

```javascript
renderer.clear();
```
```lua
renderer.clear()
```
```python
renderer.clear()
```

<code class="definition">renderer.clear()</code>

The clear function clears the currently active render target ready for new
drawing. Unless you are doing something custom, this is usually called only once 
at the beginning of a the draw event callback.

## begin

```javascript
// layer 1
renderer.begin();
renderer.set_position(50, 0);
// your draw calls go here.
renderer.present();

// layer 2.
renderer.begin(false);
// your draw calls go here.
renderer.present();
```
```lua
-- layer 1
renderer.begin()
renderer.set_position(50, 0)
-- your draw calls go here.
renderer.present()

-- layer 2
renderer.begin(false)
-- your draw calls go here.
renderer.present()
```
```python
# layer 1
renderer.begin()
renderer.set_position(50, 0)
# your draw calls go here.
renderer.present()

# layer 2
renderer.begin(false)
# your draw calls go here.
renderer.present()
```

<code class="definition">renderer.begin(<b>bool</b> reset)</code>

The begin function begins a new layer of draw calls to execute and draw onto the
currently active render target, this also resets the global transforms if reset
is set to true (true by default). This should be called typically after you call
`renderer.clear()`.

In the example on the right, false is passed to begin to retain the global 
transforms used in the first draw call.

## present

<code class="definition">renderer.present()</code>

Once you have called `renderer.begin()` and sent all of the draw calls for the 
layer, you should always finish by calling `renderer.present()`. This carries out
the draw actions you asked it to, and draws onto the currently active render
target.

## draw_texture

```javascript
renderer.draw_texture(texture_id, 0, 0, 100, 100);
```
```lua
renderer.draw_texture(texture_id, 0, 0, 100, 100);
```
```python
renderer.draw_texture(texture_id, 0, 0, 100, 100);
```

<code class="definition">renderer.draw_texture(<b>int</b> texture_id, <b>float</b> x, <b>float</b> y, <b>float</b> width, <b>float</b> height)</code>

This function is used to draw an entire texture onto part of the current render
target. Dimensions are measured in pixels, and the texture_id can be acquired by
using the [assets.load_texture](#load_texture) method.

The example on the right draws the chosen texture at 0,0. With a width and height of 100 x 100 pixels.

## draw_sub_texture

```javascript
renderer.draw_sub_texture(<b>int</b> texture_id, 0, 0, 100, 100, 0, 0, 25, 25);
```
```lua
renderer.draw_sub_texture(<b>int</b> texture_id, 0, 0, 100, 100, 0, 0, 25, 25)
```
```python
renderer.draw_sub_texture(<b>int</b> texture_id, 0, 0, 100, 100, 0, 0, 25, 25)
```

<code class="definition">renderer.draw_sub_texture(<b>int</b> texture_id, <b>float</b> dx, <b>float</b> dy, <b>float</b> dw, <b>float</b> dh, <b>float</b> sx, <b>float</b> sy, <b>float</b> sw, <b>float</b> sh)</code>

This function is used to draw part of a texture onto part of the current render
target. Dimensions are measured in pixels, and the texture_id can be acquired by
using the [assets.load_texture](#load_texture) method.

Arguments with the prefix "d" (so dx, dy etc...) are for the destination 
coordinates meaning where on the canvas the pixels will be drawn, and prefix "s" 
means source coordinates, referring to where on the texture to get pixels from.

## draw_rectangle

```javascript
renderer.draw_rectangle(20, 20, 40, 40);
```
```lua
renderer.draw_rectangle(20, 20, 40, 40)
```
```python
renderer.draw_rectangle(20, 20, 40, 40)
```

<code class="definition">renderer.draw_rectangle(<b>float</b> <b>float</b> x, <b>float</b> y, <b>float</b> width, <b>float</b> height)</code>

This function draws a coloured rectangle at the given coordinates, based on the 
colour picked when using the [renderer.set_foreground_color](#set_foreground) function.

## draw_textbox

```javascript
textbox.set_text(textbox_id, "Hello World");

renderer.draw_textbox(textbox_id);
```
```lua
textbox.set_text(textbox_id, "Hello World")

renderer.draw_textbox(textbox_id)
```
```python
textbox.set_text(textbox_id, "Hello World")

renderer.draw_textbox(textbox_id)
```

<code class="definition">renderer.draw_textbox(<b>int</b> textbox_id)</code>

This function draws a textbox that has been created using the [assets.create_textbox](#create_textbox)
function.

## draw_sprite

```javascript
renderer.draw_sprite(sprite_map_id, "walk_right", 0, 10, 10, 32, 32);
```
```lua
renderer.draw_sprite(sprite_map_id, "walk_right", 0, 10, 10, 32, 32)
```
```python
renderer.draw_sprite(sprite_map_id, "walk_right", 0, 10, 10, 32, 32)
```

<code class="definition">renderer.draw_sprite(<b>int</b> sprite_map_id, <b>string</b> group, <b>int</b> frame, <b>float</b> x, <b>float</b> y, <b>float</b> w, <b>float</b> h)</code>

This function is similar to the `draw_sub_texture` in that it draws a part of a
texture onto the screen. However instead of providing the source texture 
coordinates, you tell the function which sprite map to look in, which group, 
and which frame to get the coordinates (+ some extra info) from.

When used in combination with functions like [sprite_map.get_frame_count](#get_frame_count)
to get the number of frames available in a given sprite map group, you can easily 
introduce basic looping animations into your game.

## draw_tile_layer

```javascript
renderer.draw_tile_layer(tile_map_id, 0);
```
```lua
renderer.draw_tile_layer(tile_map_id, 0)
```
```python
renderer.draw_tile_layer(tile_map_id, 0)
```

<code class="definition">renderer.draw_tile_layer(<b>int</b> tile_map_id, <b>int</b> layer)</code>

This function tells the renderer to draw all tiles for a specific layer of a 
tile map. It's very common to need to draw things between layers of a tile map,
so this makes sure you have the control you need when doing so.

Also there are no options for position when drawing a tile layer, instead you
should use the global transform functions such as [renderer.set_position](#set_position)
to do that.

## set_background

```javascript
renderer.set_background("#000000");
```
```lua
renderer.set_background("#000000")
```
```python
renderer.set_background("#000000")
```

<code class="definition">renderer.set_background(<b>string</b> hex_color)</code>

This function lets you to set the background colour of the currently active
render target. The function expects a string with valid 6 digit HTML formatted
hex colour code, with a hash tag prefix. In the future other colour systems will
be added, so the hash tag is important.

## set_foreground

```javascript
renderer.set_foreground("#000000");
```
```lua
renderer.set_foreground("#000000")
```
```python
renderer.set_foreground("#000000")
```

<code class="definition">renderer.set_foreground(<b>string</b> hex_color)</code>

This function sets the foreground drawing colour, which is used by various other
drawing methods, such as `draw_rectangle` and `draw_textbox` (as a default if no
text colour is chosen).

The function expects a string with valid 6 digit HTML formatted
hex colour code, with a hash tag prefix. In the future other colour systems will
be added, so the hash tag is important.

## set_window_mode

```javascript
renderer.set_window_mode(0);
```
```lua
renderer.set_window_mode(0)
```
```python
renderer.set_window_mode(0)
```

<code class="definition">renderer.set_window_mode(<b>int</b> mode)</code>

This function allows you to set the window mode for the game. Here is a table of
the valid window modes available:

Mode ID | Description
------- | -----------
0 | Windowed (resizable)
1 | Full-screen
2 | Borderless Full-screen

Further modes will be added in future updates to the engine.

## set_position

```javascript
renderer.set_position(52, 33);
```
```lua
renderer.set_position(52, 33)
```
```python
renderer.set_position(52, 33)
```

<code class="definition">renderer.set_position(<b>float</b> x, <b>float</b> y)</code>

This function allows you to set the global translation coordinates for drawing.

## set_origin

```javascript
renderer.set_origin(0, 0);
```
```lua
renderer.set_origin(0, 0)
```
```python
renderer.set_origin(0, 0)
```

<code class="definition">renderer.set_origin(<b>float</b> x, <b>float</b> y)</code>

This function allows you to set the global transform origin coordinates for drawing.


## set_rotation

```javascript
renderer.set_rotation(45);
```
```lua
renderer.set_rotation(45)
```
```python
renderer.set_rotation(45)
```

<code class="definition">renderer.set_rotation(<b>float</b> angle)</code>

This function allows you to set the global rotation angle (degrees) for drawing, 
which pairs well with `set_origin`.

## set_scale

```javascript
renderer.set_scale(1, 1);
```
```lua
renderer.set_scale(1, 1)
```
```python
renderer.set_scale(1, 1)
```

<code class="definition">renderer.set_scale(<b>float</b> x, <b>float</b> y)</code>

This function allows you to set the global scale transform for drawing. Setting
both x and y to 2 for example would make all graphics you draw twice as big.

## set_shader

```javascript
renderer.set_shader(shader_id);
```
```lua
renderer.set_shader(shader_id)
```
```python
renderer.set_shader(shader_id)
```

<code class="definition">renderer.set_shader(<b>int</b> shader_id)</code>

This function sets which shader program is currently being used. Passing 0 as
the shader_id switches back to the built in shader.

## set_alpha

```javascript
renderer.set_alpha(0.5);
```
```lua
renderer.set_alpha(0.5)
```
```python
renderer.set_alpha(0.5)
```

<code class="definition">renderer.set_alpha(<b>float</b> alpha)</code>

Sets the alpha channel value (fraction between 0.0 and 1.0) to use when drawing
textures (given that blending is enabled, with the correct blend function).

By default the correct blending function is set to enable alpha-blending. However
if you change the blend function, the value you set here might have no effect.

## set_blend

```javascript
renderer.set_blend(true);
```
```lua
renderer.set_blend(true)
```
```python
renderer.set_blend(true)
```

<code class="definition">renderer.set_blend(<b>bool</b> blend)</code>

This function enables or disables the various blending features available in the
renderer. By default blending is enabled.

## set_blend_func

```javascript
renderer.set_blend_func(SRC_ALPHA, ONE_MINUS_SRC_ALPHA);
```
```lua
renderer.set_blend_func(SRC_ALPHA, ONE_MINUS_SRC_ALPHA)
```
```python
renderer.set_blend_func(SRC_ALPHA, ONE_MINUS_SRC_ALPHA)
```

<code class="definition">renderer.set_blend_func(<b>string</b> src_func, <b>string</b> dest_func)</code>

This function specifies the pixel arithmetic for blending graphics together. The
default value for src_func is `ONE`, and the default value for `dest_func` is
`ZERO`. Here is a list of the various constants that can be used with this
function:

Constant | Description
-------- | -----------
ZERO |
ONE |
SRC_COLOR |
ONE_MINUS_SRC_COLOR |
DST_COLOR |
ONE_MINUS_DST_COLOR |
SRC_ALPHA |
ONE_MINUS_SRC_ALPHA |
DST_ALPHA |
ONE_MINUS_DST_ALPHA |
CONSTANT_COLOR |
ONE_MINUS_CONSTANT_COLOR |
SRC_ALPHA_SATURATE |
SRC1_COLOR |
ONE_MINUS_SRC1_COLOR |
SRC1_ALPHA |
ONE_MINUS_SRC1_ALPHA |

## set_blend_preset

```javascript
renderer.set_blend_func(BLEND_MULTIPLY, true);
```
```lua
renderer.set_blend_func(BLEND_MULTIPLY, true)
```
```python
renderer.set_blend_func(BLEND_MULTIPLY, true)
```

<code class="definition">renderer.set_blend_preset(<b>string</b> preset_name, <b>bool</b> with_alpha)</code>

This function simplifies the blend system by allowing you to specify a blending
preset. Web browsers, and photo editing software often offer preset's as they
can be easier to understand. Here is a table of all the blend presets available.

Constant | Description
-------- | -----------
BLEND_SOURCE_OVER | 
BLEND_SOURCE_IN |
BLEND_SOURCE_OUT |
BLEND_SOURCE_ATOP |
BLEND_DESTINATION_OVER |
BLEND_DESTINATION_IN |
BLEND_DESTINATION_OUT |
BLEND_DESTINATION_ATOP |
BLEND_LIGHTER |
BLEND_COPY |
BLEND_XOR |
BLEND_MULTIPLY |
BLEND_SCREEN |
BLEND_OVERLAY |
BLEND_DARKEN |
BLEND_LIGHTEN |
BLEND_COLOR_DODGE |
BLEND_COLOR_BURN |
BLEND_HARD_LIGHT |
BLEND_SOFT_LIGHT |
BLEND_DIFFERENCE |
BLEND_EXCLUSION |
BLEND_HUE |
BLEND_SATURATION |
BLEND_COLOR |
BLEND_LUMINOSITY |