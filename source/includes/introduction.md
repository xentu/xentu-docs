# Introduction

Hi, my name is Kodaloid (Steve), and I started the Xentu project in 2018 as an 
experiment to see how performant an embedded scripting language could be for
writing entire computer games.

Web browsers have the power to enable people to build interactive experiences 
using popular scripting languages like JavaScript, Lua, Ruby & Python. But they 
come at the cost of having a big browser attached with all it's system 
requirements and overheads. I wanted to be able to take that, strip away this 
big clunky browser, and make it available to run pretty much anywhere natively.

The initial concept used C#, MonoGame and a library called NLua. The bindings 
turned out to be too slow for modern needs, though it led to a further C++ and 
native Lua experiment, which was much faster, and spawned the Xentu project as 
presented today.

## What is Xentu?

Xentu is a slim, fast and easy to learn framework for creating 2D computer 
games scripted in a variety of scripting languages, including JavaScript, Lua 
and more. It's completely free to use & publish with. It's open-source (under 
the zlib license), it's written in C/C++, and super cross-platform friendly. 
Here are some other great features:

- Draw graphics with a fully featured and fast batch renderer.
- Load textures, shaders, fonts, and more using a smart asset manager.
- Access assets from archives via the built in VFS (virtual file system).
- Input support for keyboards, mice and game pads.
- Sound and music playback, with 8 mixer tracks.
- + much more!

## Xentu vs Other Engines

The strength of Xentu is that it offers a modern cross-platform take on a 
classic native game engine, whilst adding a variety of scripting languages, and 
emphasis on code performance.

Also by implementing a strict binding API, the engine does a lot of work to 
make sure the code you write once, will work even when you run it on the 
mobile, or console versions of the engine.

If you are looking for an engine that removes barriers for sharing your games 
with people on many different platforms, Xentu has a lot to offer.

## System Requirements

Xentu has very minimal system requirements, however there are some. The main 
requirement is that the device must support OpenGL level 3.3 or higher. 
This allows the various graphical features to work correctly, such as batch 
rendering, render targets, blending and shaders.

For context, here are some examples of old devices Xentu will run fine on:

- Late 2012 Mac Mini / MacBook
- PC from 2010 with Nvidia graphics cards NV50 (Tesla+)
- PC from 2007 with AMD graphics cards R600 (Radeon HD 2000+)

There are concrete plans for ports to DirectX 9, 10, Android & iOS next year. 
And a possible port to Web Assembly. Each will change the minimums slightly and 
open doors for more devices over time.

## About This Documentation

This is a technical documentation for the Xentu game engine project. The main 
purpose it to provide explanation and guides for how to write game code to work
with the engine.

### Conventions

The documentation is split up into larger categories to help you understand how
the various parts of the game engine work. For example the [Asset System](#asset-system) 
section provides techniques on how to load assets into a game. 

Sub-headings for these sections are for most part descriptions for the various 
functions that you can call within your game code. For each function, you'll
see a function definition that looks like this:

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

This definition is pseudo-code, and should not be copied as is. It's purpose is
to explain how the function should be called. You'll usually also see to the 
right of the definition an example of how the code definition should be used.

The first part tells you that you should expect a result from the function of type
bool (or boolean). Sometimes this part including the = equals symbol is omitted
meaning the function does not return any information.

The `input.key_clicked` is the name of the function, and within the (
 round brackets ) you'll optionally see a comma separated list of arguments that 
you should pass when calling the function.

Here is a list of types that you'll commonly see in a function definition:

Type | Description
---- | -----------
bool | Boolean (true or false)
int  | Integer (signed +/-), numerical value without floating point.
enum | One of several pre-defined values (an integer under the hood).
float | Floating point numerical value.
double | Double precision floating point numerical value.
string | Represents a textual value (sequence of characters).
mixed  | Means the type can be any of the above.

### Language & Spelling Notes

This documentation is written in (British) English, however coding convention
for English speaking countries is to use American spellings for certain words. 
So in some places you may see substitutions for words like `colour` to `color` 
to maintain this convention. 

## Where are the v0.0.1 docs?

The documentation for v0.0.1 docs has been moved to the following URL: [https://docs.xentu.net/0.0.1/](https://docs.xentu.net/0.0.1/)

It will be kept live indefinitely for historic purposes, however I do not 
recommend using it as a guide for versions newer than 0.0.1 as the engine was
completely rebuilt from the ground up.

## Xentu Creator

Xentu Creator is a cross-platform, also free to use IDE (integrated development environment) built in C# on the Avalonia framework.

![First screenshot of Xentu Creator](/images/screenshots/creator-01.jpg)

It has everything you need to get started building games with Xentu. Including 
a code editor with syntax highlighting. A sprite map editor with animation 
playback. debugging, binary acquisition, game publishing and much more.

![Second screenshot of Xentu Creator](/images/screenshots/creator-02.jpg)

If you are new to Xentu, this is the best way to get started without hiccups.
Give Creator a try today by visiting the [download](https://xentu.net/download)
page.