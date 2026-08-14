---
tags:
  - linux
  - keyboard
  - stack
aliases: []
id: Input_Stack
---

## Hierarchy

- **Kernal Driver** interprets specific hardware protocols of the devices (like USB HID or I2C) and translates its signals (hardware scancode) into a standardized format (linux input keycode).
- **Kernel evdev subsystem** exposes each physical device as a `/dev/input/event*` character file.
- **libinput** is a userspace library that translates evdev events into more meaningful and high-level events like
	- pointer acceleration
	- touchpad gesture(like pinch-to-zoom and swipes)
- **Wayland Compositor** recieve the events from `libinput`. For keyboard input, the event from libinput is forwarded to `XKB` and then the XKB keysym is sent to the focused client window.
- **XKB** is a standard that defined mapping from keycode to keysym. It also modifies the events optionally (like Caps Lock to Ctrl in your Sway). `libxkbcommon` is an implementation of XKB.

> [!note]
> The keycodes in Linux console, Xorg and Wayland can be different. There is no universal standard.

> [!note] Where is `ctrl+alt+f2` handled?
> By Kernel VT Subsystem on tty and by the wayland compositor on GUI mode. When sway starts, it informs the kernel not to deal with `ctrl+alt+f2` using `ioctl(fd, KDSETMODE, KD_GRAPHIC)`. That's why when your sway hangs, you cannt `ctrl+alt+f2` to change your tty directly. But you can use `alt+SysRq` then `r` to reclaim the ownership of the keyboard from the compositor and then use `ctrl+alt+f2` because SysRq is captured before evdev. But your need to enable SysRq on your system first.

## AT & HID

- An AT keyboard has scancode. But HID keyboard only has `HID usage = (usage_page<<16) + usage_id`, which is defined in the standard, [HID Usage Tables](https://usb.org/document-library/hid-usage-tables-16). However, in sake of a uniform notation, we also call HID usage as the "scancode" of an HID keyboard.

The driver `drivers/input/keyboard/atkbd.c` maps the scancodes of an AT keyboard to keycodes. The generic HID input subsystem maps the usages of an HID keyboard to keycodes.

`udev` and `hwdb` cooperate as a supplementary component to customize some special scancode-keycode mappings for different keyboards.

You can also use `setkeycodes scancode keycode` to modify the mapping

## Tools

**evtest** monitors evdev events.
**showkey --scancodes** and **showkey --keycodes** need to run in a virtual console instead of a graphical environment
**libinput debug-events --show-keycodes** monitors libinput event
**wev** monitors the event a Wayland window received.

*Examples*:

`evtest` result:

```bash
Event: time 1754922741.745357, type 4 (EV_MSC), code 4 (MSC_SCAN), value 1e
Event: time 1754922741.745357, type 1 (EV_KEY), code 30 (KEY_A), value 1
```

`1e` is a scancode, and 30 is a linux kernel keycode.

`wev` result:

```bash
[        16:     wl_keyboard] key: serial: 1087693; time: 259297802; key: 38; state: 1 (pressed)
                      sym: a            (97), utf8: 'a'
```

38 is a XKB keycode, and `a` is a keysym(also `0x61`).

## Reference
https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450
https://wiki.archlinux.org/title/Map_scancodes_to_keycodes
https://wiki.archlinux.org/title/Keyboard_input
https://www.bilibili.com/read/readlist/rl218766
