# Input (Mouse)

## get_position

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

## button_down

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

## button_clicked

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