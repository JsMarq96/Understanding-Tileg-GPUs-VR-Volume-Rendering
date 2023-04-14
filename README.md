# Understanding Tiled Mobile GPUs throught VR Volume Rendering

## NOTE: This is a WIP, the structure and data are due to change in the coming months; and corrections are always appreciated  :)

## Why

There is a lot of dogmatism and hearsay in the area of Computer Graphics, specially in the area of mobile GPUs. And it does not help that one of the biggest players in this hardware space (Qualcomm) is a *really* closed ecosystem, with not a lot of public documentation. This hardware is usually quite different from their desktop counterparts, with a distinct (tiled) infrastructure. Wich brings a new set of constraints to the table: it is not just a less powerfull version than its desktop counterparts.

My goal is to better understand the strenghts & limitations of this hardware via empirical testing & debuging tools. I plan to do this throught the lens of stereoscopic volume rendering.

## The platform

Since there is a lot of variablity between manufacturers of mobile GPUs, I decided to go with the most ubiquous one, Qualcomm and their Snapgradragon XR2 SOC; in the Meta Quest 2 device.

My reasoning for this is straightworward: is the most ubiquouts and accessible XR device, and that allowed Qualcomm to stay as the de-facto chip maker for XR mobile-powered devices; and researching volume rendering in this aplication can bring benefits to more cost efective VR medical platforms.

This poses some problems, like the absolute absense of official documentation of the SOC, best practices, and this sort of techniques.

It also offers some interesting capabilities, in the form of Qualcomm's exclusive extensions, for Variable Rate Shadding, Frame Reprojection, Foveated Rendering, and so.

## The metodology

The main idea is to asses the cost of different rendering techiques, and try to remedy the issues of their implementation, and how they scale, the more percentage of the viewport is filled with the volume rendering in question.

The volume that is going to be presented is the ubiquous bonsai 3D texture, and I am going to center in rendering an Isosurface, since when trying to achieve a volumetric or spectral representation there is not a lot of manouverability with the cost.

The tecnhiques present some old aproaches, revisited in this paradigm; some usual suspects; and more mother aproaches:

* Raymarching
* MipMap Accelerated Raymarching
* Volumetric Billboards
* Surface nets
* Octree based rendering

If time allows, It would also be interesting how effective can be the different more traditional VR techniques on top of this list; like Foveated Rendering.

Using the RenderDoc Meta Fork, it is posible to obtain quite a lot of low-level information, in a per-drawcall matter, such as:

* Frame times
* Clocks
* Texture cache misses: L1, L2, total rates
* Total number of bytes read from memmory
* ALU usage per vertex/fragment
* EFU usage per vertex/fragment
* Fragments shaded
* Usage per viewport tile

This can help paint the cost of each different technique; in different viewport configurations.

In order to reduce noise, the perspective for each test will be fixed, and the results will be averaged between multiple samples.

## The test enviorment

The main enviorment is in OpenGL ES 3.3, due its comparable features to OpenGL 4.0; and since this tests are not in a complex scene, with different materials and messhes, I determined that the benefits of working in Vulkan in this set of test could be negligible (at least in most test).

This tests have been ran in a Meta Quest 2, with software version XXX and with the performance indicator for both CPU & GPU set to maximun.

The test will be done for each algorithm in a set of already stablished and fixed view positions, changing the size of the volume representation in the viewport.

(TODO add the viewport examples)

## Tiled GPUs

*on progress*

## Tecnhiques

* [Raymarching](https://github.com/JsMarq96/Understanding-Tileg-GPUs-VR-Volume-Rendering/blob/main/raymarching/raymarching.md)
* [Mipmap Accelerated Raymarching](https://github.com/JsMarq96/Understanding-Tileg-GPUs-VR-Volume-Rendering/blob/main/mipmap-accel-raymarching/mar.md)

## Repositories

* [Desktop, OpenGL 4.0 implementation](https://github.com/JsMarq96/Volume-Rendering-Desktop)
* [Quest, OpenGL ES 3.3 implementation](https://github.com/JsMarq96/Quest-Tiled-Volume-Rendering)
