---
tags:
  - GPU
  - hardware
  - stack
aliases: []
id: Linux_Graphics_Stack
---

## Hierarchy

- **Kernel-space drivers**, like `radeon`, `i915`, `nouveau` communicate directly with GPU by writing registers, accessing video memory directly, e.t.c. But the driver can only serve exclusively for a single process at a time.[^1]
- **DRM/DRI** (Direct Rendering Manager/Infrastructure) manages the context for multiple processes (because hardware registers and memory are global resources). But they expose GPU interfaces mostly as-is, not in a vendor-neural portable way.
- **Vendor-neutral user-space driver**, like OpenGL, Direct3D, Vulkan and Metal, provides a general interface. It also includes VDPAU (NVIDIA & AMD) and VA-API(AMD & Intel) for video hardware acceleration.
- **Wayland compositor**, like KWin for KDE, talks to DRM/DRI directly[^6] to compose windows into a harmonic desktop. It utilizes EGL(formerly GLX) to share and receive data from multiple contexts like OpenGL and OpenVG.[^2] Some compositors use wlroots to help with rendering like sway. Desktop effects are rendered by software or hardware.[^3]
- **GUI framework**, like Qt, GTK, draws windows by software or hardware.[^4] And then pass the framebuffer to Wayland compositor.[^2]

*By software or hardware*: the program can use CPU to draw pictures on memory or use vendor-neutral user-space driver to draw pictures on video memory(or memory if it's embedded GPU).

## Facts

**Mesa** is an open source implementation of a collection of user-space drivers, including OpenGL ES, OpenCL, VDPAU, VA-API, Vulkan and EGL, for different GPUs. But it does not implement Direct3D and Metal. Gallium3D is a modular driver framework in Mesa connecting different user-space drivers and kernel-space drivers. However, Gallium3D does not support Vulkan directly because Vulkan is stateless. Zink Driver translates Gallium3D to Vulkan. One can imagine that future drivers within Mesa only implement Vulkan and rely on Zink for OpenGL compatibility.[^5]

**Chromium** on linux uses GTK to draw the window frame, native dialogs, e.t.c for a better theme integration and **Skia** (GUI framework) to draw web page content. Formerly, Skia has different backends for OpenGL, Vulkan, e.t.c. Now google is developing **Graphite Engine** which unifies different backends. 
- Old Path: Skia -> OpenGL Backend -> OpenGL -> Driver -> GPU
- New Path (Graphite): Skia -> Graphite Engine -> Vulkan or Metal -> Driver -> GPU

**JavaScript APIs** provide web-safe invocations to user-space drivers in a browser. The translator is ANGLE in chromium.
- WebGL -> OpenGL ES 2.0
- WebGL2 -> OpenGL ES 3.0
- WebGPU -> Vulkan, Metal, DirectX 12

[^1]: [trying to understand drm dri mesa radeon gallium](https://www.reddit.com/r/archlinux/comments/6la6n5/trying_to_understand_drm_dri_mesa_radeon_gallium/)
[^2]: [why wayland is using opengl es instead of opengl](https://unix.stackexchange.com/questions/511134/why-wayland-is-using-opengl-es-instead-of-opengl)
[^3]: [Desktop Effects Performance](https://userbase.kde.org/Desktop_Effects_Performance)
[^4]: [Qt OpenGL](https://doc.qt.io/qt-6/qtopengl-index.html)
[^5]: [The Linux graphics stack in a nutshell, Part 1](https://lwn.net/Articles/955376/)
[^6]: [The Linux graphics stack in a nutshell, Part 2](https://lwn.net/Articles/955708/)
[^7]: [【OpenGL 篇】为什么游戏总要编译着色器？](https://www.bilibili.com/video/BV1zi421h7tJ/)
