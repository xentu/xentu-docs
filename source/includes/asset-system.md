# Asset System

Asset loading in Xentu is done via the `assets` global. In this section we'll
explore how to use the asset system when building games.

Before that, here are some useful tips when using the asset manager:

- Loaders are blocking by nature, so they can hang the game if you try to load a large asset (like some music, text file, or a big texture).
- Some loaders return an integer instead of data, this integer is a throw-away pointer linking to the data to speed up processing.
- Cached data is automatically cleaned up when your game shuts down, however there are methods to do this manually too (prefixed with `delete_`).

## assets.mount

<code class="definition">assets.mount(<b>string</b> point, <b>string</b> path)</code>

```javascript
assets.mount("/second", "/second.zip");

// then mount point is available, and can be used like this:
const id = assets.load_texture("/second/tex01.png");
```
```lua
assets.mount("/second", "/second.zip")

-- then mount point is available, and can be used like this:
id = assets.load_texture("/second/tex01.png")
```
```python
assets.mount("/second", "/second.zip")

# then mount point is available, and can be used like this:
id = assets.load_texture("/second/tex01.png")
```

Xentu has a custom VFS (virtual file system) that allows assets to be loaded
traditionally, or from within zip archives.

The way it works is Xentu is aware only of file systems or archives that are
mounted. By default `./` and `./assets` are mounted, which is how the engine
can locate `game.json`.

Here are some rules that should be observed:

- Only files connected to mounts can be loaded.
- Absolute filenames do not work, they are invisible to Xentu.
- First file gets priority when a duplicate exists on multiple mounts.

These rules are a little unusual, however they add several benefits. For example
rogue code can not directly access the filesystem without a deliberate mount,
mods can be made possible, and packaging your game becomes a lot more straight 
forward.

<aside class="notice">
<b>Hint:</b> The <code>/assets</code> mount can be a folder or zip file. And <code>game.json</code>
can sit inside.
</aside>

## assets.read_text_file

<code class="definition">assets.read_text_file(<b>string</b> path)</code>

```javascript
const text = assets.read_text_file("/text_file.txt");
```
```lua
text = assets.read_text_file("/text_file.txt")
```
```python
text = assets.read_text_file("/text_file.txt")
```

This method is a reliable way for reading textual source from a file in the VFS,
and supports modern text encoding.

A lot of other methods in the engine take advantage of this method. For example, 
a good way to load a shader is to read two shader files using this. Then
pass the source code into `assets.load_shader(v, s)`.

The text that is loaded does not get cached, so make sure to store it somewhere
as a variable in your game code after calling this.

There is no file type restriction as long as it can be interpreted as a string
by the language engine.

## assets.load_texture

<code class="definition">assets.load_texture(<b>string</b> path)</code>

```javascript
const texture_id = assets.read_text_file("/textures/example.png");
```
```lua
texture_id = assets.read_text_file("/textures/example.png")
```
```python
texture_id = assets.read_text_file("/textures/example.png")
```

Xentu currently uses the SDL_Image library for loading texture data into the
engine. This library states that it can load BMP, GIF, JPEG, LBM, PCX, PNG, PNM
(PPM/PGM/PBM), QOI, TGA, XCF, XPM, and simple SVG format images.

When calling load_texture, you receive a texture_id that can be used in many of
the draw methods explored later in this documentation.

## assets.load_font

<code class="definition">assets.load_font(<b>string</b> path, <b>int</b> size)</code>

```javascript
const font_id = assets.load_font("/fonts/arial.ttf", 20);
```
```lua
font_id = assets.load_font("/fonts/arial.ttf", 20)
```
```python
font_id = assets.load_font("/fonts/arial.ttf", 20)
```

The initial version of this engine had only support for sprite fonts, however
Xentu now supports loading of true type font files directly from the
VFS.

When you load a font, a size is also requested so that a sprite font can be
generated. Due to this, like loading a texture, this loader also gives you an
asset id.

<aside class="warning">
Make sure to only use fonts that you have permission to use. Many of the fonts
that come with your computer are copyrighted.
</aside>

## assets.load_sound

<code class="definition">assets.load_sound(<b>string</b> path)</code>

```javascript
const sound_id = assets.load_sound("/sounds/fx01.wav");
```
```lua
sound_id = assets.load_sound("/sounds/fx01.wav")
```
```python
sound_id = assets.load_sound("/sounds/fx01.wav")
```

The type of audio you can load into your game highly depends on what you've 
setup in the `game.json` file, which is why configuration of that file is so
important.

If for example you set the audio frequency to 48kHz but then load a WAV file
that is encoded at 44.1kHz, or you load audio with a different bit depth, you 
will very likely experience unpredictable behaviour.

Sound files can be in any of the formats you enable in `game.json`, however they
must be short enough to store as a sample, rather than streamed audio.

## assets.load_music

<code class="definition">assets.load_music(<b>string</b> path)</code>

```javascript
const music_id = assets.load_music("/music/track01.ogg");
```
```lua
music_id = assets.load_music("/music/track01.ogg")
```
```python
music_id = assets.load_music("/music/track01.ogg")
```

Same rules apply to music as sound loading from above. Make sure to match the
audio settings you specify in `game.json` and you should be fine.

The main difference between sound files and music, is that music is stored as a
stream-able source, and is played over a long period of time, with optimizations
to make sure it does not interfere with the visual aspect of the game.

Music files can be in any of the formats you enable in `game.json`, however they
must be long enough to store as a stream-able source.

## assets.load_shader

<code class="definition">assets.load_shader(<b>string</b> vert, <b>string</b> frag)</code>

```javascript
const shader1_vert = assets.read_text_file("/shaders/shader1.vert");
const shader1_frag = assets.read_text_file("/shaders/shader1.frag");
const shader1_id = assets.load_shader(shader1_vert, shader1_frag);
```
```lua
shader1_vert = assets.read_text_file("/shaders/shader1.vert")
shader1_frag = assets.read_text_file("/shaders/shader1.frag")
shader1_id = assets.load_shader(shader1_vert, shader1_frag)
```
```python
shader1_vert = assets.read_text_file("/shaders/shader1.vert")
shader1_frag = assets.read_text_file("/shaders/shader1.frag")
shader1_id = assets.load_shader(shader1_vert, shader1_frag)
```

> Here is what the built in shader looks like:

```glsl
#version 330

in vec3 i_position;
in vec2 i_texcoord;
in vec4 i_color;
uniform mat4 u_MVP;
out vec2 v_TexCoord;
out vec4 v_Color;
void main()
{
	gl_Position = u_MVP * vec4(i_position, 1.0); 
	v_TexCoord = i_texcoord;
	v_Color = i_color;
}

# frag shader

in vec2 v_TexCoord;
in vec4 v_Color;
uniform sampler2D u_Texture;
out vec4 frag_colour;
void main()
{
	vec4 texColor = texture(u_Texture, v_TexCoord);
	frag_colour = texColor * v_Color;
}
```

Xentu currently runs on SDL 2 with OpenGL 3.3 extensions, which means the 
shaders you can load in should be written in GLSL, and match shader version 330
or higher.

For our purpose, a shader program is made up of two common types. A vertex, and
a fragment shader, which need to be compiled into a single program before you can
use them.

In the example, you get a shader_id out of the load_shader function which can be 
used to switch between shader programs during draw calls.

### Why use shaders?

There is a limited amount that you can do by just loading in textures into a 
game. Shaders enable you to add visual modification that would not be possible
without them.

A good example might be transitions between scenes with special effects. You
could implement basic lighting. Day/night cycle in an RPG, the possibilities are
limitless if you put the time in.

### Communicating with a shaders

Xentu has special functions for communicating with a shader to pass it extra
information. A link will appear here once the documentation for them has been
added.

## assets.load_sprite_map

<code class="definition">assets.load_sprite_map(<b>string</b> path)</code>

```javascript
const map_id = assets.load_sprite_map("/sprite_maps/map1.xsf");
```
```lua
map_id = assets.load_sprite_map("/sprite_maps/map1.xsf")
```
```python
map_id = assets.load_sprite_map("/sprite_maps/map1.xsf")
```

> Example of an XSF file:

```json
{
  "image": "/images/ZOMBIE_1.png",
  "animations": [
    {
      "name": "walk_right",
      "frames": [
        { "delay": 100, "coords": "0, 0, 25, 25" },
        { "delay": 100, "coords": "25, 0, 25, 25" },
        { "delay": 100, "coords": "50, 0, 25, 25" },
        { "delay": 100, "coords": "75, 0, 25, 25" }
      ]
    }
  ]
}
```

XSF Sprite Map's are special JSON formatted files that describe regions and
animations that can be found within a texture.

Xentu Creator provides a tool for creating these XSF files, though their 
composition is very easy to understand.

When an XSF file is loaded using this method, you receive an asset id for the
map. Also the texture specified as "image" is loaded behind the scenes in a
managed space, where if the sprite map is removed from the asset manager, that underlying image data gets removed as well.

These files are very important when building games, as they allow you to get
animation into the game with very little time investment.

## assets.create_textbox

<code class="definition">assets.create_textbox(<b>float</b> x, <b>float</b> y, <b>float</b> w, <b>float</b> h)</code>

```javascript
const textbox_id = assets.create_textbox(10, 10, 300, 90);
```
```lua
textbox_id = assets.create_textbox(10, 10, 300, 90)
```
```python
textbox_id = assets.create_textbox(10, 10, 300, 90)
```

Drawing text is expensive in computer games. So to mitigate some many of the 
performance penalties, Xentu uses a system that predefines surfaces on which 
text can be measured, and drawn.

So to draw text, we first need to create textbox areas using this method. The
argument specified remain fixed whilst the textbox exists, however a textbox is
affected by global transforms, so you can move, size and rotate in other ways.

## assets.unload_texture

<code class="definition">assets.unload_texture(<b>int</b> asset_id)</code>

Unload a texture.

```javascript
assets.unload_texture(texture0);
```
```lua
assets.unload_texture(texture0)
```
```python
assets.unload_texture(texture0)
```

## assets.unload_font

<code class="definition">assets.unload_font(<b>int</b> asset_id)</code>

Unload a font.

```javascript
assets.unload_font(font0);
```
```lua
assets.unload_font(font0)
```
```python
assets.unload_font(font0)
```

## assets.unload_sound

<code class="definition">assets.unload_sound(<b>int</b> asset_id)</code>

Unload a sound.

```javascript
assets.unload_sound(sound0);
```
```lua
assets.unload_sound(sound0)
```
```python
assets.unload_sound(sound0)
```

## assets.unload_music

<code class="definition">assets.unload_music(<b>int</b> asset_id)</code>

Unload music.

```javascript
assets.unload_music(music0);
```
```lua
assets.unload_music(music0)
```
```python
assets.unload_music(music0)
```

## assets.unload_shader

<code class="definition">assets.unload_shader(<b>int</b> asset_id)</code>

Unload a shader.

```javascript
assets.unload_shader(shader0);
```
```lua
assets.unload_shader(shader0)
```
```python
assets.unload_shader(shader0)
```

## assets.unload_sprite_map

<code class="definition">assets.unload_sprite_map(<b>int</b> asset_id)</code>

Unload a sprite map.

```javascript
assets.unload_sprite_map(spriteMap0);
```
```lua
assets.unload_sprite_map(spriteMap0)
```
```python
assets.unload_sprite_map(spriteMap0)
```