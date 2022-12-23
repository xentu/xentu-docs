# The Basics

## How It Works

The Xentu game engine at it's core is a program (or binary) that you run on a 
computer. If you just run the program, it will start up then close immediately 
as it does not know what to do. So to make it do something more useful, you 
need to provide it with some instructions.

When the binary runs, it actually wants to find a file called `game.json` which
contains the game configuration. The engine uses the built in virtual file system
to find this file, which by default looks in either `./` or `./assets`.

<aside class="notice">
<b>Important:</b> Xentu binaries are sensitive to the executing path.
</aside>

This means if you make the binary available via a system environment path, Xentu 
will look in the path you are browsing, not the path where the binary is 
placed.
<br /><br />
This is used extensively in Xentu Creator allowing you to create games without
needing to have multiple copies of the executable.


## Game Folder Structure

The most common layout for a game in Xentu looks like this:

Name | Description
---- | -----------
/game.json | Your configuration file.
/game.js | Your main code file as described by entry_point in `game.json` (can also be .lua or .py).
/textures/ | A folder to place your textures in.
/includes/ | A folder to place extra code files.

You can add many extra code files, however it's important to remember to use the
same code language when you do. Xentu supports 1 coding language per game, which
is decided when your `game.json` file is first loaded.


## The game.json File

> Here is an example of a `game.json` file.

```json
{
	"game": {
		"title": "Hello World",
		"entry_point": "/game.js",
		"version": "0.0.0",
		"v_sync": true,
		"fullscreen": false,
		"update_frequency": 60,
		"draw_frequency": 60,
		"window": {
			"width": 1280,
			"height": 720
		},
		"viewport": {
			"width": 500,
			"height": 500,
			"mode": 1
		},
		"audio": {
			"frequency": 44100,
			"channels": 2,
			"depth": 16,
			"codecs": ["wav", "ogg", "flac"]
		}
	}
}
```

On the right you'll see an example of how this `game.json` file should look.
The main object should always be called `game`, and the subordinate properties
should follow the pattern you see in the example. Here is a rundown summary on what each property does:

Property | Description
-------- | -----------
title | The title of your game.
entry_point | The file that contains your code, can be of type `.js` or `.lua` see the next section [Hello World](#hello-world) on what code should go in this file.
version | The version of your game.
v_sync | Whether or not to enable v-sync.
fullscreen | Whether or not to start the game in full-screen mode.
update_frequency | Specify how many times a second to call the update event.
draw_frequency | Specify a target draw calls per second (0 for unlimited).
window | Specifies the size (width and height) of the window to create.
viewport | Specifies the size (width and height) of the draw target.
audio | Tells the engine what kind of audio to expect.

### Viewport Mode

The viewport property has a third property called `mode`. This property tells the
engine how to handle a viewport that does not neatly fit into the size of the 
window. Here are the options you can give it:

Mode | Description
---- | -----------
0 | Stick to top-left of window (default).                                   
1 | Position centre of the window.
2 | Stretch viewport to size of the window.

The game window by default is resizable, making this option very important if you
have a specific look in mind.

### Audio Options

Here is a description of the various audio options that you can specify:


Property | Description
-------- | -----------
frequency | Specify the audio frequency (default 44100)
channels | The number of audio channels, either 1, 2 or 4 (default 2)
depth | The bit-depth of the audio, either 8, 16, or 24 (default 16)
codecs | Choose which codecs are used. Pick from wav, ogg, flac, mp3, midi or mod (by default only wav is enabled)

Note that some of these options can reduce performance, and some may not even
work on certain devices. Only verge from the defaults if you absolutely sure
you know what you are doing.

<aside class="notice">
<b>Important:</b> Using mp3 requires a license that does not come with the
engine. Only enable the feature if you have one, or are exempt.
</aside>

## Hello World

```javascript
// Source code for game.js

print("Hello from javascript!");

// assets
texture0 = assets.load_texture("/texture0.png");

// variables
renderer.set_background("#444444");

// handle the init event
game.on("init", function() {
	print("Initialized!");
});

// handle the update event
game.on("update", function(dt) {
	if keyboard.key_clicked(KB_ESCAPE) {
		game.exit();
	}
})

// handle the draw event
game.on("draw", function(dt) {
	renderer.clear();
	renderer.begin();
	renderer.draw_texture(texture0, 10, 10, 100, 100);
	renderer.present();
})
```

```lua
-- Source code for game.lua

print("Hello from lua!")

-- assets
texture0 = assets.load_texture("/texture0.png")

-- variables
renderer.set_background("#444444")

-- handle the init event
game.on("init", function()
	print("Initialized!")
end)

-- handle the update event
game.on("update", function(dt)
	if keyboard.key_clicked(KB_ESCAPE) then
		game.exit()
	end
end)

-- handle the draw event
game.on("draw", function(dt)
	renderer.clear()
	renderer.begin()
	renderer.draw_texture(texture0, 10, 10, 100, 100)
	renderer.present()
end)
```

```python
# Source code for game.py

print("Hello from python!")

# assets
texture0 = assets.load_texture("/texture0.png")

# variables
renderer.set_background("#444444")

# handle the init event
def init():
	print("Initialized!")
	
# handle the update event
def update(dt):
	if keyboard.key_clicked(KB_ESCAPE):
		game.exit()

# handle the draw event
def draw(dt):
	renderer.clear()
	renderer.begin()
	renderer.draw_texture(texture0, 10, 10, 100, 100)
	renderer.present()
```

It's traditional to include a Hello World example, to demonstrate what a basic
example of a project looks like, so here is what a basic game would look like
written in Xentu.

This example prints the text "Hello from [language]!", loads a texture from an
image file called `texture0.png`. Then sets the background colour to the HTML 
hex code `#444444` (dark grey). It also watches for the escape key to be pressed
to exit, and draws the loaded texture at coordinates [10,10,100,100] once per 
draw call.

This documentation provides examples for every language supported. Use the tabs
at the top right of this website to select the code language you wish to see
examples for.

Currently the most popular language for writing games in Xentu is JavaScript. 
The engine also allows Lua (and soon Python).

Each of the supported languages have the same features available, though some
languages provide their own benefits. For example JavaScript has a more familiar
and easy to read syntax, while Lua and Python have shorthand tricks up their 
sleeve for getting more done with less code.

## Events

Xentu uses an event system for communicating engine events to your script code.
For example when the engine wants to draw a frame, it sends a draw event to 
your code, so that you can decide what to draw at that given moment.

## The init event

```javascript
// handle the init event
game.on("init", function() {
	print("Initialized!");
});
```

```lua
-- handle the init event
game.on("init", function()
	print("Initialized!")
end)
```

```python
# handle the init event
def init():
	print("Initialized!")
```

This event fires before any other event is fired, and it indicates that things
like timers, assets and the renderer are ready to start.

In the examples above you will see textures are loaded before this is fired, and 
that is ok, because this event is most useful to indicate readiness, and 
sometimes you want to wait while things like assets load before starting your 
own code.


## The update event

```javascript
// handle the update event
game.on("update", function(dt) {
	if keyboard.key_clicked(KB_ESCAPE) {
		game.exit();
	}
})
```

```lua
-- handle the update event
game.on("update", function(dt)
	if keyboard.key_clicked(KB_ESCAPE) then
		game.exit()
	end
end)
```

```python	
# handle the update event
def update(dt):
	if keyboard.key_clicked(KB_ESCAPE):
		game.exit()
```

The update event fires to request game logic from your code. You can specify how
frequently this is called using the `update_frequency` property in your 
`game.json`.

This event provides a single argument called `dt` that specifies how much time 
(in seconds, with floating point precision) has passed since the last update 
event was fired.


## The draw event

```javascript
// handle the draw event
game.on("draw", function(dt) {
	renderer.clear();
	renderer.begin();
	renderer.draw_texture(texture0, 10, 10, 100, 100);
	renderer.present();
})
```

```lua
-- handle the draw event
game.on("draw", function(dt)
	renderer.clear()
	renderer.begin()
	renderer.draw_texture(texture0, 10, 10, 100, 100)
	renderer.present()
end)
```

```python
# handle the draw event
def draw(dt):
	renderer.clear()
	renderer.begin()
	renderer.draw_texture(texture0, 10, 10, 100, 100)
	renderer.present()
```

The draw event fires when the engine wants to draw a new frame onto the screen.
Like the update event, the draw event can also be controlled in the `game.json`
file with properties `draw_frequency` and `v_sync`.

This event also has a similar argument called `dt` that indicates how much time
has passed since the last draw event was fired.

### Draw Call Order

It is useful to know that `renderer.clear()` clears the screen. `renderer.begin()` 
begins a new batch of rendering, and `renderer.present()` sends that batch to the
GPU for drawing.

If you call multiple pairs of `begin()` and `present()` calls, you effectively
get the ability to draw layers, which can be very useful when building the visual
hierarchy of your game.


## The key_down event

```javascript
// handle the draw event
game.on("key_down", function(key_code) {
	print("key down " + key_code.toString());
})
```
```lua
-- handle the draw event
game.on("key_down", function(key_code)
   print("key down " .. key_code)
end)
```
```python
# handle the draw event
def key_down(key_code):
	print("key down " + str(key_code))
```

The key_down event tells you when a key on the keyboard has been pressed. As this
is buffered, it is recommended that you use the [keyboard.key_down](#keyboard-key_down) 
function instead if you need to know immediately when a key is pressed.

## The key_click event

```javascript
// handle the draw event
game.on("key_click", function(key_code) {
	print("key clicked " + key_code.toString());
})
```
```lua
-- handle the draw event
game.on("key_click", function(key_code)
   print("key clicked " .. key_code)
end)
```
```python
# handle the draw event
def key_down(key_code):
	print("key down " + str(key_code))
```

The key_click event tells you when a key on the keyboard has been clicked (meaning
that the key was pressed, then released).

## Custom Events

> The code below should output to the console "my_event was triggered!"

```javascript
// handle the custom event.
game.on("my_event", function(arg0) {
	print(arg0);
});

// trigger an event.
game.trigger("my_event", "my_event was triggered!");
```

```lua
-- handle the custom event.
game.on("my_event", function(arg0)
	print(arg0)
end)

-- trigger an event.
game.trigger("my_event", "my_event was triggered!")
```

```python
# implement event handler.
def my_event_handler(arg0):
	print(arg0)

# hook custom event handler.
game.on("my_event", "my_event_handler")

# trigger an event.
game.trigger("my_event", "my_event was triggered!")
```

Events can be a great way of routing game logic, so Xentu allows you to create
and subscribe to custom events just like you saw above.

Python is the main outlier here, as you need to define a function before you can
use `game.on(event, callback)`.