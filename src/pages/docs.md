---
title: Docs
layout: layouts/docs.njk
permalink: /Docs/
eleventyNavigation:
  key: Docs
  order: 1
---

## Introduction

usdtweak is a free and open source editor for Pixar's [USD](https://graphics.pixar.com/usd/release/index.html#) format. The project is still in early stage, but usdtweak can already be used for small and simple tasks like cleaning assets, creating and editing layers or inspecting and fixing existing usd stages.

This project is written in C++ and relies on [ImGUI](https://github.com/ocornut/imgui) for the UI and [GLFW](https://github.com/glfw/glfw) for the windowing system.

## Sneak peek

![screenshot1](https://media.giphy.com/media/9Nb4JmmqEXzO05DpvL/giphy.gif)

## Status

There is no roadmap at the moment, as it is my side project and the development is slow and unpredictable, I can only work on it a few hours during the week-end. The original idea behind this project was to improve usdview by adding edition capabilities, for artists, technical directors and users who don't necessarily know the USD ascii syntax or are not familiar with python. So my current goal driving the developments is to provide at least the same functionalities as usdview and some ability to edit the stages and layers.

As of today usdtweak allows

- to edit multiple stages and layers at the same time, copying and pasting prims between layers,
- to edit stages properties selecting the edit target
- to edit layer hierarchy: adding, deleting, reparenting, and renaming prims
- to edit layer stack: adding, deleting new sublayers
- to create and delete compositions like variants, references and payloads, inherits, ...
- to change property values in layers or stages
- to add and delete keys
- a minimal viewport interaction: translating, rotating, scaling objects.
- text editing (for small files)
- and more ...

Drop me an email if you are interested in beta testing on windows or if you can't compile it.

## Building

### Requirement

The project is almost self contained and only needs:

- [cmake](https://cmake.org/) installed (version > 3.14)
- a C++14 compiler installed: MSVC 19 or 17, g++ or clang++.
- a build of [Universal Scene Description](https://github.com/PixarAnimationStudios/USD/releases/tag/v22.05) version >= 20.11. (I am not sure the USD libraries provided with maya, houdini or omniverse would work)

If you managed to build USD, compiling usdtweak should be easy, cmake needs only 1 required variables:

- **pxr_DIR** pointing to the USD installation directory containing the file pxrConfig.cmake

### Compiling on linux

On linux it should compile with:

    git clone https://github.com/cpichard/usdtweak
    cd usdtweak
    git checkout develop
    mkdir build
    cd build
    cmake -Dpxr_DIR=/installs/usd-22.05 ..
    make

### Compiling on MacOs

It compiles on MacOs Catalina. The viewport doesn't work as the required OpenGL version is not supported, but the layer editor does.

    git clone https://github.com/cpichard/usdtweak
    cd usdtweak
    git checkout develop
    mkdir build
    cd build
    cmake -Dpxr_DIR=/installs/usd-22.05 ..
    make

### Compiling on Windows

It should compile successfully on Windows 10 with MSVC 19 or 17 using the RelWithDbInfo config. Make sure you open/use the x64 Native Tools commands prompt before typing the following commands:

    git clone https://github.com/cpichard/usdtweak
    cd usdtweak
    git checkout develop
    mkdir build
    cd build
    cmake  -G "Visual Studio 16 2019" -A x64 -Dpxr_DIR=C:\installs\usd-22.05 ..
    cmake --build . --config RelWithDebInfo

### Installing on Windows

You can install usdtweak with its dependencies on windows, it copies the required files in a directory with the following command:

    cmake --install . --prefix <where_you_want_to_install_usdtweak> --config RelWithDebInfo

Note that it is not really tested on anything else than my machine/setup so it might not work for you, feel free to get in touch if you have any issue.

### Creating a Windows installer

There is an experimental packaging system using cpack/NSIS on windows which creates an installer. You have to make sure the nsis application is available on you system, you can download it from here [NSIS](https://nsis.sourceforge.io/Download). The command to create the installer is then:

    cmake --build . --target package --config RelWithDebInfo

### Compiling with your version of glfw

usdtweak is using [GLFW](https://www.glfw.org/) for its windowing system. cmake should normally download, compile and install glfw without any user intervention. However, if you already have a compiled version you want to use instead, and you'll need to disable the automatic build of glfw, by passing an additional cmake variable:

- **glfw3_DIR** pointing to your GLFW installation directory and containing the file glfw3Config.cmake

A cmake command will then look like:

    cmake  -G "Visual Studio 16 2019" -A x64 -Dpxr_DIR=C:\installs\usd-21.11 -Dglfw3_DIR=C:\installs\glfw3-3.3.6\lib\cmake\glfw3 ..

## Contact

If you want to know more, or have any issues, questions, drop me an email: cpichard.github@gmail.com
