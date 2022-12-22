# Renderer

Explains all of the methods available from the rendering engine. 

## renderer.clear

<code class="definition">renderer.clear()</code>

## renderer.begin

<code class="definition">renderer.begin()</code>

## renderer.present

<code class="definition">renderer.present()</code>

## renderer.draw_texture

<code class="definition">renderer.draw_texture(<b>int</b> texture_id, <b>float</b> x, <b>float</b> y, <b>float</b> width, <b>float</b> height)</code>

## renderer.draw_sub_texture

<code class="definition">renderer.draw_sub_texture(<b>int</b> texture_id, <b>float</b> dx, <b>float</b> dy, <b>float</b> dw, <b>float</b> dh, <b>float</b> sx, <b>float</b> sy, <b>float</b> sw, <b>float</b> sh)</code>

## renderer.draw_rectangle

<code class="definition">renderer.draw_rectangle(<b>float</b> <b>float</b> x, <b>float</b> y, <b>float</b> width, <b>float</b> height)</code>

## renderer.draw_textbox

<code class="definition">renderer.draw_textbox(<b>int</b> textbox_id)</code>

## renderer.draw_sprite

<code class="definition">renderer.draw_sprite(<b>int</b> sprite_map_id, <b>string</b> group, <b>int</b> frame, <b>float</b> x, <b>float</b> y, <b>float</b> w, <b>float</b> h)</code>

## renderer.set_background

<code class="definition">renderer.set_background(<b>string</b> hex_color)</code>

## renderer.set_foreground

<code class="definition">renderer.set_foreground(<b>string</b> hex_color)</code>

## renderer.set_window_mode

<code class="definition">renderer.set_window_mode(<b>int</b> mode)</code>

## renderer.set_position

<code class="definition">renderer.set_position(<b>float</b> x, <b>float</b> y)</code>

## renderer.set_origin

<code class="definition">renderer.set_origin(<b>float</b> x, <b>float</b> y)</code>

## renderer.set_rotation

<code class="definition">renderer.set_rotation(<b>float</b> angle)</code>

## renderer.set_scale

<code class="definition">renderer.set_scale(<b>float</b> x, <b>float</b> y)</code>

## renderer.set_shader

<code class="definition">renderer.(<b>int</b> shader_id)</code>

## renderer.set_alpha

<code class="definition">renderer.set_alpha(<b>float</b> alpha)</code>

## renderer.set_blend

<code class="definition">renderer.set_blend(<b>bool</b> blend)</code>

## renderer.set_blend_func

<code class="definition">renderer.set_blend_func(<b>string</b> func_name)</code>

## renderer.set_blend_preset

<code class="definition">renderer.set_blend_preset(<b>string</b> preset_name)</code>