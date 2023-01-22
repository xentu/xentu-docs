# Input (Keyboard)

Xentu provides support for various forms of user input via the `input` global
object. In this section you'll see a breakdown of how to interact with the 
keyboard, mouse and a gamepad.

## key_down

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


## key_clicked

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