# Audio System

Explains how the audio system works in Xentu.

## play_sound

```javascript
audio.play_sound(audio0, -1, 0);
```
```lua
audio.play_sound(audio0, -1, 0)
```
```python
audio.play_sound(audio0, -1, 0)
```

<code class="definition">audio.play_sound()</code>

## play_music

```javascript
audio.play_music(music0, 0);
```
```lua
audio.play_music(music0, 0)
```
```python
audio.play_music(music0, 0)
```

<code class="definition">audio.play_music()</code>

## stop_sound

```javascript
audio.stop_sound();
```
```lua
audio.stop_sound()
```
```python
audio.stop_sound()
```

<code class="definition">audio.stop_sound()</code>

## stop_music

```javascript
audio.stop_music();
```
```lua
audio.stop_music()
```
```python
audio.stop_music()
```

<code class="definition">audio.stop_music()</code>

## set_sound_volume

```javascript
audio.set_sound_volume(sound0, 0.5);
```
```lua
audio.set_sound_volume(sound0, 0.5)
```
```python
audio.set_sound_volume(sound0, 0.5)
```

<code class="definition">audio.set_sound_volume(<b>int</b> sound_id, <b>float</b> volume)</code>

## set_channel_volume

```javascript
audio.set_channel_volume(0, 0.5);
```
```lua
audio.set_channel_volume(0, 0.5)
```
```python
audio.set_channel_volume(0, 0.5)
```

<code class="definition">audio.set_channel_volume(<b>int</b> channel_id, <b>float</b> volume)</code>

## set_music_volume

```javascript
audio.set_music_volume(0.5);
```
```lua
audio.set_music_volume(0.5)
```
```python
audio.set_music_volume(0.5)
```

<code class="definition">audio.set_music_volume(<b>float</b> volume)</code>

## set_channel_panning

```javascript
audio.set_channel_panning(channel_id, 0, 0);
```
```lua
audio.set_channel_panning(channel_id, 0, 0)
```
```python
audio.set_channel_panning(channel_id, 0, 0)
```

<code class="definition">audio.set_channel_panning(<b>int</b> channel_id, <b>float</b> left, <b>float</b> left)</code>