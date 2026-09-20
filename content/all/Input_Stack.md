---
id: Input_Stack
title: Input_Stack
aliases: []
tags:
  - linux
  - keyboard
  - stack
---

## Hierarchy

- **Kernal Driver** interprets specific hardware protocols of the devices (like USB HID or I2C) and translates its signals (hardware scancode) into a standardized format (linux input keycode).
- **Kernel evdev subsystem** exposes each physical device as a `/dev/input/event*` character file.
- [*keyboard*](https://cdn.kernel.org/doc/html/latest/input/input.html#keyboard) is an in-kernel input handler and is a part of VT code. It is on the same level as `evdev`
- **libinput** is a userspace library that translates evdev events into more meaningful and high-level events like pointer acceleration and touchpad gesture(like pinch-to-zoom and swipes). It does not change the keycode.
- **Wayland Compositor** uses `libinput` to deal with the received evdev and get `wl_keyboard.key`, which is a a platform-specific key code that can be interpreted by feeding it to the keyboard mapping like `xkb_v1`.
- **Wayland Client** interpret the `wl_keyboard.key` in the appropriate keymapping to get the XKB keysym(e.g. Control_L), XKB modifier(e.g. Control).
- **XKB** is a standard that defined mapping from keycode to keysym. It also modifies the events optionally (like Caps Lock to Ctrl in your Sway). `libxkbcommon` is an implementation of XKB.

> [!note] Where is `ctrl+alt+f2` handled?
> By Kernel VT Subsystem on tty and by the wayland compositor on GUI mode. When sway starts, it informs the kernel not to deal with `ctrl+alt+f2` using `ioctl(fd, KDSETMODE, KD_GRAPHIC)`. That's why when your sway hangs, you cannt `ctrl+alt+f2` to change your tty directly. But you can use `alt+SysRq` then `r` to reclaim the ownership of the keyboard from the compositor and then use `ctrl+alt+f2` because SysRq is captured before evdev. But your need to enable SysRq on your system first.

**showkey --scancodes** and **showkey --keycodes** need to run in a virtual console instead of a graphical environment

Monitor codes:
- hardware-specific: HID usage, AT scancode. `showkey --scancodes`, `evtest`
- Linux-specific
    - keyboard: `showkey --keycodes`
    - evdev keycode: `evtest`
    - libinput: `libinput debug-events --show-keycodes`
    - wl_keyboard.key: `WAYLAND_DEBUG=1 wev`
- XKB-specific: XKB keycode = evdev + 8. `wev`
- layout-spacific: keysym. `wev`

> [!note] ctrl:nocaps vs caps:ctrl_modifier
> In XKB, The former maps caps to keysym = Control_L and modifier = Control while the latter maps caps to keysym = Caps_Lock and modifier = Control. A wayland client still getwl_keyboard.key. That's why even when using ctrl:nocaps, `KeyboardEvent.code` in a browser still recognizes the caps. You can check it out [here](00-Attachments/multifractal.html)

## AT & HID

- An AT keyboard has scancode. But HID keyboard only has `HID usage = (usage_page<<16) + usage_id`, which is defined in the standard, [HID Usage Tables](https://usb.org/document-library/hid-usage-tables-16). However, in sake of a uniform notation, we also call HID usage as the "scancode" of an HID keyboard.

The driver `drivers/input/keyboard/atkbd.c` maps the scancodes of an AT keyboard to keycodes. The generic HID input subsystem maps the usages of an HID keyboard to keycodes.

`udev` and `hwdb` cooperate as a supplementary component to customize some special scancode-keycode mappings for different keyboards.

You can also use `setkeycodes scancode keycode` to modify the mapping

## Reference
https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450
https://wiki.archlinux.org/title/Map_scancodes_to_keycodes
https://wiki.archlinux.org/title/Keyboard_input
https://www.bilibili.com/read/readlist/rl218766
