# Getting Started

## Introduction

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
And a port to WASM in 2024. Each will change the minimums slightly and open 
doors for more devices over time.

# Xentu Creator

Xentu Creator is a cross-platform, also free to use IDE (integrated development environment) built in C# on the Avalonia framework.

![First screenshot of Xentu Creator](/images/screenshots/creator-01.jpg)

It has everything you need to get started building games with Xentu. Including 
a code editor with syntax highlighting. A sprite map editor with animation 
playback. debugging, binary acquisition, game publishing and much more.

![Second screenshot of Xentu Creator](/images/screenshots/creator-02.jpg)

If you are new to Xentu, this is the best way to get started without hiccups.
Give Creator a try today by visiting the [download](https://xentu.net/download)
page.