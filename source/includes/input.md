# Input

Xentu provides support for various forms of user input via the `input` global
object. In this section you'll see a breakdown of how to interact with the 
keyboard, mouse and a gamepad.

## keyboard.key_down

```javascript
if (keyboard.key_down(KB_ESCAPE)) {
	// do something.
}
```
```lua
if keyboard.key_down(KB_ESCAPE) then
	-- do something.
end
```
```python
if keyboard.key_down(KB_ESCAPE):
	# do something.
```

<code class="definition"><b>bool</b> result = input.key_down(<b>int</b> keycode)</code>

Detect if a key on the keyboard is pressed down. Here is a list of the available 
key codes:

Constants | ..  | ..    
--------- | --- | ---
KB_SPACE | KB_V | KB_F12
KB_APOSTROPHE | KB_W | KB_F13
KB_COMMA | KB_X | KB_F14
KB_MINUS | KB_Y | KB_F15
KB_PERIOD | KB_Z | KB_F16
KB_SLASH | KB_LEFT_BRACKET | KB_F17
KB_1 | KB_BACKSLASH | KB_F18
KB_2 | KB_RIGHT_BRACKET | KB_F19
KB_3 | KB_GRAVE_ACCENT | KB_F20
KB_4 | KB_ESCAPE | KB_F21
KB_5 | KB_ENTER | KB_F22
KB_6 | KB_TAB | KB_F23
KB_7 | KB_BACKSPACE | KB_F24
KB_8 | KB_INSERT | KB_KP_1
KB_9 | KB_DELETE | KB_KP_2
KB_0 | KB_RIGHT | KB_KP_3
KB_SEMICOLON | KB_LEFT | KB_KP_4
KB_EQUAL | KB_DOWN | KB_KP_5
KB_A | KB_UP | KB_KP_6
KB_B | KB_PAGE_UP | KB_KP_7
KB_C | KB_PAGE_DOWN | KB_KP_8
KB_D | KB_HOME | KB_KP_9
KB_E | KB_END | KB_KP_0
KB_F | KB_CAPS_LOCK | KB_KP_DECIMAL
KB_G | KB_SCROLL_LOCK | KB_KP_DIVIDE
KB_H | KB_NUM_LOCK | KB_KP_MULTIPLY
KB_I | KB_PRINT_SCREEN | KB_KP_SUBTRACT
KB_J | KB_PAUSE | KB_KP_ADD
KB_K | KB_F1 | KB_KP_ENTER
KB_L | KB_F2 | KB_KP_EQUAL
KB_M | KB_F3 | KB_LEFT_SHIFT
KB_N | KB_F4 | KB_LEFT_CONTROL
KB_O | KB_F5 | KB_LEFT_ALT
KB_P | KB_F6 | KB_LEFT_SUPER
KB_Q | KB_F7 | KB_RIGHT_SHIFT
KB_R | KB_F8 | KB_RIGHT_CONTROL
KB_S | KB_F9 | KB_RIGHT_ALT
KB_T | KB_F10 | KB_RIGHT_SUPER
KB_U | KB_F11 | KB_MENU


## keyboard.key_clicked

```javascript
if (keyboard.key_clicked(KB_ESCAPE)) {
	// do something.
}
```
```lua
if keyboard.key_clicked(KB_ESCAPE) then
	-- do something.
end
```
```python
if keyboard.key_clicked(KB_ESCAPE):
	# do something.
```

<code class="definition"><b>bool</b> result = input.key_clicked(<b>int</b> keycode)</code>

Detect when a key on the keyboard is clicked. Which is detected by checking if
the specified key was previously pressed, and was released since the last update
call was made.

## mouse.get_position

```javascript
const mp = mouse.get_position();
// mp.x
// mp.y
```
```lua
mp_x, mp_y = mouse.get_position()
```
```python
mp_x, mp_y = mouse.get_position()
```

<code class="definition"><b>mixed</b> result = mouse.get_position()</code>

Get the x,y coordinates of the mouse cursor on the game canvas.

## mouse.button_down

```javascript
if (mouse.button_down(0)) {
	// do something.
}
```
```lua
if mouse.button_down(0) then
	-- do something.
end
```
```python
if mouse.button_down(0):
	# do something.
```

<code class="definition"><b>bool</b> result = mouse.button_down(<b>int</b> button_index)</code>

Detect if a mouse button is pressed down. The available constants for `button_index`
are `MOUSE_LEFT`, `MOUSE_RIGHT` and `MOUSE_MIDDLE`.

## mouse.button_clicked

```javascript
if (mouse.button_clicked(MOUSE_LEFT)) {
	// do something.
}
```
```lua
if mouse.button_clicked(MOUSE_LEFT) then
	-- do something.
end
```
```python
if mouse.button_clicked(MOUSE_LEFT):
	# do something.
```

<code class="definition"><b>bool</b> result = mouse.button_clicked(<b>int</b> button_index)</code>

Detect when a mouse button is clicked.  Which is detected by checking if
the specified button was previously pressed, and was released since the last 
update call was made.


## gamepad.get_axis

```javascript
const mp = gamepad.get_axis(0);
// mp.x
// mp.y
```
```lua
gp_x, gp_y = gamepad.get_axis(0)
```
```python
gp_x, gp_y = gamepad.get_axis(0)
```

<code class="definition"><b>mixed</b> result = gamepad.get_axis(<b>int</b> gamepad_index)</code>

When a gamepad is connected, this function returns the x and y direction of the
(traditionally left) thumb stick. The values returned are either 1, 0 or -1 only.
If 0 is returned, it means that the thumb stick is within the dead zone.

## gamepad.get_axis_raw

```javascript
const mp = gamepad.get_axis_raw(0);
// mp.x
// mp.y
```
```lua
gp_x, gp_y = gamepad.get_axis_raw(0)
```
```python
gp_x, gp_y = gamepad.get_axis_raw(0)
```

<code class="definition"><b>mixed</b> result = gamepad.get_axis_raw(<b>int</b> gamepad_index)</code>

When a gamepad is connected, this function returns the raw x and y direction of the
(traditionally left) thumb stick. The values returned are set to a range between
-32768 to -8000, 0 and 8000 to 32767. If 0 is returned, it means that the thumb
stick is within the dead zone.

## gamepad.button_down

```javascript
if (gamepad.button_down(0, 0)) {
	// do something.
}
```
```lua
if gamepad.button_down(0, 0) then
	-- do something.
end
```
```python
if gamepad.button_down(0, 0):
	# do something.
```

<code class="definition"><b>bool</b> result = gamepad.button_down(<b>int</b> gamepad_index, <b>int</b> button_index)</code>

Detect if a specific gamepad's button is pressed down.

## gamepad.button_clicked

```javascript
if (gamepad.button_clicked(0, 0)) {
	// do something.
}
```
```lua
if gamepad.button_clicked(0, 0) then
	-- do something.
end
```
```python
if gamepad.button_clicked(0, 0):
	# do something.
```

<code class="definition"><b>bool</b> result = gamepad.button_clicked(<b>int</b> gamepad_index, <b>int</b> button_index)</code>

Detect if a specific gamepad's button has been clicked