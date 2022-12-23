# Textbox


```javascript
font0 = assets.load_font("/fonts/Roboto-Regular.ttf", 20);
text0 = assets.create_textbox(10, 10, 680, 40);

textbox.set_text(text0, font0, "Hello World");
textbox.set_color(text0, font0, "#FFFF00");

game.on("draw", function(dt) {
	renderer.clear();
	renderer.begin();
	renderer.draw_textbox(text0);
	renderer.present();
});
```
```lua
font0 = assets.load_font("/fonts/Roboto-Regular.ttf", 20)
text0 = assets.create_textbox(10, 10, 680, 40)

textbox.set_text(text0, font0, "Hello World")
textbox.set_color(text0, font0, "#FFFF00")

game.on("draw", function(dt)
	renderer.clear();
	renderer.begin();
	renderer.draw_textbox(text0);
	renderer.present();
end)
```
```python
font0 = assets.load_font("/fonts/Roboto-Regular.ttf", 20)
text0 = assets.create_textbox(10, 10, 680, 40)

textbox.set_text(text0, font0, "Hello World")
textbox.set_color(text0, font0, "#FFFF00")

def draw(dt):
	renderer.clear()
	renderer.begin()
	renderer.draw_textbox(text0)
	renderer.present()
```

Drawing text is expensive in computer games. So to mitigate some many of the 
performance penalties, Xentu uses a system that predefines surfaces on which 
text can be measured, and drawn onto objects called textboxes.

You can create a textbox using the asset system function [assets.create_textbox](#assets-create_textbox)
Once you've created a textbox, you can interact with it by using the functions
in this section.

On the right is an example of how a textbox is created, then used.

## textbox.set_text

```javascript
textbox.set_text(text0, font0, "Hello World");
```
```lua
textbox.set_text(text0, font0, "Hello World")
```
```python
textbox.set_text(text0, font0, "Hello World")
```

<code class="definition">textbox.set_text(<b>int</b> textbox_id, <b>int</b> font_id, <b>string</b> text)</code>

Sets the text and font that should appear on a textbox when rendered.

## textbox.set_color

```javascript
textbox.set_color(text0, font0, "#FFFF00");
```
```lua
textbox.set_color(text0, font0, "#FFFF00")
```
```python
textbox.set_color(text0, font0, "#FFFF00")
```

<code class="definition">textbox.set_text(<b>int</b> textbox_id, <b>string</b> hex)</code>

Sets the text colour for a textbox when rendered. 

## textbox.measure_text

```javascript
const result = textbox.measure_text(text0, font0, "Hello World");
// result.x
// result.y
```
```lua
width, height = textbox.measure_text(text0, font0, "Hello World")
```
```python
width, height = textbox.measure_text(text0, font0, "Hello World")
```

<code class="definition">textbox.measure_text(<b>int</b> textbox_id, <b>int</b> font_id, <b>string</b> text)</code>

Returns the measured dimensions of the text that has been set onto a textbox.