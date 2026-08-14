---
id: audio_stack
title: audio_stack
aliases: []
tags:
  - linux
  - music
  - audio
  - stack
---

## Hierarchy

- **ALSA** provides the necessary **kernel** drivers for sound cards. OSS is its predecessor.
- **Sound Servers** manage and routes audio streams from different applications and control the volume.
    - PulseAudio is designed for general desktop use. It is easy to use.
    - JACK is designed for professional audio work.
    - PipeWire is a newer multimedia framework, aiming to unify the capabilities of both PulseAudio and JACK.
- Applications

## Useful commands

*Old-school*:
- Display all sound cards: `cat /proc/asound/cards`
- Display all PCM devices: `cat /proc/asound/pcm`
- Display supported inputs of a sound card: `cat /proc/asound/card1/stream0`
- Display current working states: `cat /proc/asound/card1/pcm0p/sub0/hw_params`

*Modern*:
- `wpctl status`
- `pw-top`

## Terminology

- ALSA
    - `period_size`: how many samples are processed in each hardware interrupt.
    - `buffer_size = period_size * periods`.
    - `period_time = (period_size / rate) × 1,000,000`.
- Sound Server (You can see the following columes in `pw-top`)
    - `quant`(quantum): number of frames processed per processing cycle in a PipeWire graph. For example, if `quant=1024` and `period=512`, the PipeWire graph runs only once every two hardware periods.

`pcm0p`, `pcm1c` signify the device 0 for playback(p) and device 1 for capture(c). `sub` distinguishes subdevices in multi-channel independent audio streams. The caveat here is that subdevices are used for hardware mixing instead of in charge of different channels. For example, for a 5.1 surround sound setup you would have a single playback PCM device and only 1 subdevice (instead of 6).

## Reference
- https://wiki.archlinux.org/title/PipeWire
- https://docs.pipewire.org/index.html
- https://docs.pipewire.org/page_man_pipewire_1.html
