# Events

Xentu uses an event system for communicating engine events to your script code.
For example when the engine wants to draw a frame, it sends a "draw" event to 
your code. If you decide to handle that event, you can define a "callback" function
to decide what to draw at that given moment.

A single event can have multiple subscribed callback functions, which can be
useful if you wish a chain of things to happen when an event is triggered.

The order in which those callback functions are ran is determined based on the
order in which you subscribe to an event.

In this section we'll look at some events that are triggered automatically by the
engine.

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
// handle the key_down event
game.on("key_down", function(key_code) {
	print("key down " + key_code.toString());
})
```
```lua
-- handle the key_down event
game.on("key_down", function(key_code)
   print("key down " .. key_code)
end)
```
```python
# handle the key_down event
def key_down(key_code):
	print("key down " + str(key_code))
```

The key_down event tells you when a key on the keyboard has been pressed. As this
is buffered, it is recommended that you use the [keyboard.key_down](#keyboard-key_down) 
function instead if you need to know immediately when a key is pressed.

## The key_click event

```javascript
// handle the key_down event
game.on("key_click", function(key_code) {
	print("key clicked " + key_code.toString());
})
```
```lua
-- handle the key_down event
game.on("key_click", function(key_code)
   print("key clicked " .. key_code)
end)
```
```python
# handle the key_down event
def key_down(key_code):
	print("key down " + str(key_code))
```

The key_click event tells you when a key on the keyboard has been clicked (meaning
that the key was pressed, then released).


## The window_changed event

```javascript
// handle the window_changed event
game.on("window_changed", function(event_name) {
	if (event_name == 'size_changed') {
		print("The window has been changed!");
	}
})
```
```lua
-- handle the window_changed event
game.on("window_changed", function(event_name)
	if event_name == 'size_changed' then
		print("The window has been changed!")
	end
end)
```
```python
# handle the window_changed event
def window_changed(event_name):
	if event_name == 'size_changed':
		print("The window has been changed!")
```

The window_change event fires when something happens to the window containing 
your game. Here is a list of the various event names that can be passed to your
callback:

Event | Description
----- | -----------
size_changed | When the window size changes.
shown | The window is shown to the user.
hidden | The window is hidden.
moved | The window has been moved.
minimized | The window is minimized.
maximized | The window is maximised.
restored | The window is restored from a maximised or minimised state.
enter | The mouse has entered.
leave | The mouse has left.
focus | The window has gained keyboard focus.
blur | The window has lost keyboard focus.

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