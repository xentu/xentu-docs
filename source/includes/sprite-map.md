# Sprite Maps

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

Sprite maps allow you to divide a larger image up into identifiable sprite 
regions (or animations) and frames. This is really useful as sprites can be
small, so having a lot on a single texture can be super efficient for drawing
lots of graphics at once.

Xentu provides a sprite map file type called XSF written in an easy to understand
JSON format.

These XSF files can be loaded through the asset system via the function 
[assets.load_sprite_map](#assets-load_sprite_map), which also conveniently loads 
the underlying texture, and auto-disposes once finished.

Xentu Creator provides all the tools you need for creating, and testing sprite
maps.

## sprite_map.get_frame_info

```javascript
var fi = sprite_map.get_frame_info(sprite_map_id, "walk_right", 0);
```
```lua
fi_delay, fi_flip_x, fi_flip_y = sprite_map.get_frame_info(sprite_map_id, "walk_right", 0)
```
```python
fi_delay, fi_flip_x, fi_flip_y = sprite_map.get_frame_info(sprite_map_id, "walk_right", 0)
```

<code class="definition">mixed = sprite_map.get_frame_info(<b>int</b> sprite_map_id, <b>string</b> group, <b>int</b> frame)</code>

This function retrieves information about a frame on a sprite map frame. Info
returned includes a delay value for how many milliseconds should be waited until 
the next frame should be shown in an animation, and two booleans that identify
whether a graphic is drawn flipped on the x or y axis.

## sprite_map.get_frame_count

```javascript
var count = sprite_map.get_frame_count(sprite_map_id, "walk_right");
```
```lua
count = sprite_map.get_frame_count(sprite_map_id, "walk_right")
```
```python
count = sprite_map.get_frame_count(sprite_map_id, "walk_right")
```

<code class="definition">count = sprite_map.get_frame_count(<b>int</b> sprite_map_id, <b>string</b> group)</code>

This function retrieves the number of frames stored in a sprite map group.