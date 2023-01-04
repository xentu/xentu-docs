# Tile Maps

At the most basic description, a tile map is a system for describing an arranged
grid of drawable tiles. It's common for computer games to use this sort of thing,
as it provides a convenient and performant way of organising a 2d scene.

Tile maps are also very easy to represent in data, making it possible to store
in a computer file ready to be loaded into a game when desired. 

Modern tile maps contain far more than just a set of tiles however. For instance
a tile map can be split up into a series of layers. For which each can have a 
extra information, such as a list of polygons, variables, text areas etc... 

Due to how integral these sorts of structures can be when creating 2d games, 
Xentu provides built-in support for them out of the box. Including an asset 
loader method for the popular TMX tile map file format, a rendering method for
drawing layers, and functions for reading and writing to the tile maps you load.

This section describes those functions, and demonstrates how to use them. To see
how a tile map can be loaded, please visit the [Asset System](#asset-system) 
section. And to see how to draw a tile layer, visit the [renderer.draw_tile_layer()](#renderer-draw_tile_layer)
section.


## tile_map.get_layer

```javascript
const layer_info = tile_map.get_layer(tile_map_id, layer_id);
```
```lua
layer_info = tile_map.get_layer(tile_map_id, layer_id)
```
```python
layer_info = tile_map.get_layer(tile_map_id, layer_id)
```

<code class="definition"><b>dict</b> result = tile_map.get_layer(<b>int</b> tile_map_id, <b>int</b> layer_id)</code>

This function gives you a way to read a collection of property variables for a
tile map layer. The first argument is the id of the tile map you loaded, and the
layer_id is the numerical index of the layer to retrieve info for.

## tile_map.get_layer_tiles

```javascript
const tiles = tile_map.get_layer_tiles(tile_map_id, layer_id);
```
```lua
tiles = tile_map.get_layer_tiles(tile_map_id, layer_id)
```
```python
tiles = tile_map.get_layer_tiles(tile_map_id, layer_id)
```

<code class="definition"><b>array</b> result = tile_map.get_layer_tiles(<b>int</b> tile_map_id, <b>int</b> layer_id)</code>

This function retrieves a raw integer array of tile indices associated with a 
tile map layer. This can be useful for a number of reasons, however it is not
required for just drawing a tile map. For that see the [renderer.draw_tile_layer()](#renderer-draw_tile_layer) 
function.


## tile_map.get_layer_objects

```javascript
const objects = tile_map.get_layer_objects(tile_map_id, layer_id);
```
```lua
objects = tile_map.get_layer_objects(tile_map_id, layer_id)
```
```python
objects = tile_map.get_layer_objects(tile_map_id, layer_id)
```

<code class="definition"><b>array</b> result = tile_map.get_layer_objects(<b>int</b> tile_map_id, <b>int</b> layer_id)</code>

This function returns an array of objects associated with a tile layer. Here is
a list of built in properties you can expect to see for each object:

Property Name | Persistence | Description
------------- | ----------- | -----------
id | always | The numeric id of the object.
name | always | The name of the object.
class | always | Used by some to define extra classification for an object.
type | always | The type of object (see below).
x | optional | The x coordinate for the object.
y | optional | The y coordinate for the object.
width | optional | The width of the object.
height | optional | The height of the object.
visible | optional | Weather the object should be visible.
points | optional | Used if type is polygon or point, describes a series of relative 2d point coordinates.
text | optional | Text for the object when the type is text.
font_family | optional | The name of the font family when the type is 'text'.
font_size | optional | The size of the font when the type is 'text'.
tile_id | optional | The idx of the tile to draw when the type is 'tile'.

If optional appears in the persistence column, it means that the field is provided
under a certain condition. An object can be one of the following types (described
by the `type` property):

Object Type | Description
----------- | -----------
rectangle | A closed 2-D polygon, having 4 sides, 4 corners, and 4 right angles.
point | An individual point in 2d space.
ellipse | A closed curve that fills the rectangular area of the object.
polygon | A set of relative 2d points, which may make up a closed shape.
tile | A single tile that can be drawn individually.
text | Represents an area of text.

## tile_map.get_tile

```javascript
const tile_info = tile_map.get_tile(tile_map_id, layer_id, tile_id);
```
```lua
tile_info = tile_map.get_tile(tile_map_id, layer_id, tile_id)
```
```python
tile_info = tile_map.get_tile(tile_map_id, layer_id, tile_id)
```

<code class="definition"><b>dict</b> result = tile_map.get_tile(<b>int</b> tile_map_id, <b>int</b> layer_id, <b>int</b> tile_id)</code>

Gets a keyed array of associated variables for an individual tile.

## tile_map._get_object

```javascript
const tile_info = tile_map.get_object(tile_map_id, layer_id, object_id);
```
```lua
tile_info = tile_map.get_object(tile_map_id, layer_id, object_id)
```
```python
tile_info = tile_map.get_object(tile_map_id, layer_id, object_id)
```

<code class="definition"><b>dict</b> result = tile_map.get_object(<b>int</b> tile_map_id, <b>int</b> layer_id, <b>int</b> object_id)</code>

Gets a single object from a tile map layer, see above for a definition of the
information you can expect to be returned.

## tile_map.change_layer

```javascript
tile_map.change_layer(tile_map_id, layer_id, "opacity", 0.4);
```
```lua
tile_map.change_layer(tile_map_id, layer_id, "opacity", 0.4)
```
```python
tile_map.change_layer(tile_map_id, layer_id, "opacity", 0.4)
```

<code class="definition">tile_map.change_layer(<b>int</b> tile_map_id, <b>int</b> layer_id, <b>string</b> prop, <b>string</b> value)</code>

Use this function to change the property value for a layer.

## tile_map.change_tile

```javascript
tile_map.change_tile(tile_map_id, layer_id, "name", "New Name");
```
```lua
tile_map.change_tile(tile_map_id, layer_id, "opacity", "New Name")
```
```python
tile_map.change_tile(tile_map_id, layer_id, "opacity", "New Name")
```

<code class="definition">tile_map.change_tile(<b>int</b> tile_map_id, <b>int</b> layer_id, <b>int</b> tile_id, <b>string</b> prop, <b>string</b> value)</code>

Use this function to change the property value for a tile on a layer.

## tile_map_change_object

```javascript
tile_map.change_object(tile_map_id, layer_id, object_id, "name", "New Name");
```
```lua
tile_map.change_object(tile_map_id, layer_id, object_id, "opacity", "New Name")
```
```python
tile_map.change_object(tile_map_id, layer_id, object_id, "opacity", "New Name")
```

<code class="definition">tile_map.change_object(<b>int</b> tile_map_id, <b>int</b> layer_id, <b>int</b> object_id, <b>string</b> prop, <b>string</b> value)</code>

Use this function to change the property value for a tile on a layer. Note that
some properties such as id and type are read only and can not be changed.