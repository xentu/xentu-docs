# Tile Maps

Sprite maps allow you to divide a larger image up into identifiable sprite 
regions (or animations) and frames. This is really useful as sprites can be
small, so having a lot on a single texture can be super efficient for drawing
lots of graphics at once.

## tile_map.get_layer

<code class="definition">tile_map.get_layer(tm, layer)</code>

## tile_map.get_layer_tiles

<code class="definition">tile_map.get_layer_tiles(tm, layer)</code>

## tile_map.get_layer_objects

<code class="definition">tile_map.get_layer_objects(tm, layer)</code>

## tile_map.get_layer_polygons

<code class="definition">tile_map.get_layer_polygons(tm, layer)</code>

## tile_map.get_tile

<code class="definition">tile_map.get_tile(tm, layer, tile)</code>

## tile_map_get_object

<code class="definition">tile_map_get_object(tm, layer, object)</code>

## tile_map_change_layer

<code class="definition">tile_map_change_layer(tm, layer, prop, val)</code>

## tile_map_change_tile

<code class="definition">tile_map_change_tile(tm, layer, tile, prop, val)</code>

## tile_map_change_object

<code class="definition">tile_map_change_object(tm, layer, obj, prop, val)</code>