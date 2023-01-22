# Input (Gamepad)

## get_axis

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

## get_axis_raw

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

## button_down

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

## button_clicked

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