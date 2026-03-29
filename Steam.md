---
title: Gamescope
description: 
published: true
date: 2026-03-28T18:11:05.412Z
tags: 
editor: markdown
dateCreated: 2025-03-29T20:28:47.784Z
---



# What Is Gamescope
* a lightweight compositor
* Software sits between game and actual display
* A virtual monitor or display for games

# Installation 
```
sudo dnf install gamescope
```

# Command and Argument Information
to run a game with Gaemscope you need to add `gamescope` to the beginning
of the steam arguements. `gamescope -- %command%`

## Gamescope help command
Help command can be run through the terminal
`gamescope --help`

## Common Launch Options
These are commands that would be commonly used by users.
Resolutions listed a bit large due to ultra wide monitor testing

### Adjust Ouput Width/Height
* Solves issues where, game refuses to run at the preferred resolution
* Often an issue on ultra wide monitors
    * We may want the game not to take on default fullscreen behavior
    * Game ooutput options can be wonky
```
gamescope -W 3840 -H 2160  -b -- %command%
```
`-b` removes border from the window

### Enable HDR
* HDR (High Dynamic Range) enhances picture by expanding the color range available.
* HDR rendering requires compatible game, and display
* For the flag to work properly you will likely need to enable HDR within OS enviroment
```
gamescope --hdr-enabled -- %command%
```

### Enable FSR
```
gamescope -F fsr -- %command%
```

### Force Grab Mouse
* When a game is not full screen the mouse cursor may escape the game window
* The mouse can be forced to stay within the boundry of the game window
```
gamescope --force-grab-cursor -- %command%
```

# Gamescope Flags Reference (AI Formated)

## General Options

| Flag | Short | Description |
|------|-------|-------------|
| `--help` | | Show help message |
| `--output-width` | `-W` | Output width |
| `--output-height` | `-H` | Output height |
| `--nested-width` | `-w` | Game width |
| `--nested-height` | `-h` | Game height |
| `--nested-refresh` | `-r` | Game refresh rate (frames per second) |
| `--max-scale` | `-m` | Maximum scale factor |
| `--scaler` | `-S` | Upscaler type: `auto`, `integer`, `fit`, `fill`, `stretch` |
| `--filter` | `-F` | Upscaler filter: `linear`, `nearest`, `fsr`, `nis`, `pixel` |
| `--sharpness`, `--fsr-sharpness` | | Upscaler sharpness from `0` (max) to `20` (min) |
| `--expose-wayland` | | Support Wayland clients using xdg-shell |
| `--mouse-sensitivity` | `-s` | Multiply mouse movement by given decimal number |
| `--backend` | | Rendering backend: `auto` (default), `drm`, `sdl`, `headless`, `wayland` |
| `--cursor` | | Path to default cursor image |
| `--ready-fd` | `-R` | Notify FD when ready |
| `--rt` | | Use realtime scheduling |
| `--stats-path` | `-T` | Write statistics to path |
| `--hide-cursor-delay` | `-C` | Hide cursor image after delay |
| `--steam` | `-e` | Enable Steam integration |
| `--xwayland-count` | | Create N xwayland servers |
| `--prefer-vk-device` | | Prefer Vulkan device for compositing (e.g. `1002:7300`) |
| `--force-orientation` | | Rotate the internal display: `left`, `right`, `normal`, `upsidedown` |
| `--force-windows-fullscreen` | | Force windows inside gamescope to be the size of the nested display |
| `--cursor-scale-height` | | Base output height to linearly scale the cursor against |
| `--virtual-connector-strategy` | | Specifies how to make virtual connectors |
| `--adaptive-sync` | | Enable adaptive sync / variable rate refresh if available |
| `--framerate-limit` | | Simple framerate limit (divisor of refresh rate). Default: `0` (disabled) |
| `--mangoapp` | | Launch with mangoapp (MangoHud) performance overlay enabled |

## HDR Options

| Flag | Description |
|------|-------------|
| `--hdr-enabled` | Enable HDR output (requires Gamescope WSI layer). Without this, HDR clients are tonemapped to SDR |
| `--sdr-gamut-wideness` | Set the 'wideness' of the SDR gamut. Range: `0`–`1` |
| `--hdr-sdr-content-nits` | Luminance of SDR content in nits. Default: `400` |
| `--hdr-itm-enabled` | Enable SDR→HDR inverse tone mapping (SDR input only) |
| `--hdr-itm-sdr-nits` | SDR content luminance for inverse tone mapping. Default: `100`, Max: `1000` |
| `--hdr-itm-target-nits` | Target luminance for inverse tone mapping. Default: `1000`, Max: `10000` |

## Nested Mode Options

| Flag | Short | Description |
|------|-------|-------------|
| `--nested-unfocused-refresh` | `-o` | Game refresh rate when unfocused |
| `--borderless` | `-b` | Make the window borderless |
| `--fullscreen` | `-f` | Make the window fullscreen |
| `--grab` | `-g` | Grab the keyboard |
| `--force-grab-cursor` | | Always use relative mouse mode instead of flipping on cursor visibility |
| `--display-index` | | Force gamescope to use a specific display in nested mode |

## Embedded Mode Options

| Flag | Short | Description |
|------|-------|-------------|
| `--prefer-output` | `-O` | List of connectors in order of preference (e.g. `DP-1,DP-2,HDMI-A-1`) |
| `--default-touch-mode` | | `0`: hover, `1`: left, `2`: right, `3`: middle, `4`: passthrough |
| `--generate-drm-mode` | | DRM mode generation algorithm: `cvt`, `fixed` |
| `--immediate-flips` | | Enable immediate flips (may result in tearing) |

## Debug Options

| Flag | Description |
|------|-------------|
| `--disable-layers` | Disable libliftoff (hardware planes) |
| `--debug-layers` | Debug libliftoff |
| `--debug-focus` | Debug XWM focus |
| `--synchronous-x11` | Force X11 connection synchronization |
| `--debug-hud` | Paint HUD with debug info |
| `--debug-events` | Debug X11 events |
| `--force-composition` | Disable direct scan-out |
| `--composite-debug` | Draw frame markers on alternating corners when compositing |
| `--disable-color-management` | Disable color management |
| `--disable-xres` | Disable XRes for PID lookup |
| `--hdr-debug-force-support` | Force HDR support even if the display doesn't support it (output will still be SDR) |
| `--hdr-debug-force-output` | Force HDR10 PQ output even if unsupported (will look wrong if not supported) |
| `--hdr-debug-heatmap` | Display a heatmap debug view of HDR luminance across the scene in nits |

## Reshade Shader Options

| Flag | Description |
|------|-------------|
| `--reshade-effect` | Name of a reshade shader from `/usr/share/gamescope/reshade/Shaders` or `~/.local/share/gamescope/reshade/Shaders` |
| `--reshade-technique-idx` | Technique index to use from the reshade effect |

## Steam Deck Options

| Flag | Description |
|------|-------------|
| `--mura-map` | Set the mura compensation map for the display (path to map file) |

## Platform Options

| Flag | Description |
|------|-------------|
| `--allow-deferred-backend` | Allow initting the backend in a deferred way (minor correctness compromises) |
| `--keep-alive` | Keep Gamescope alive even after the primary process dies |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Super + F` | Toggle fullscreen |
| `Super + N` | Toggle nearest neighbour filtering |
| `Super + U` | Toggle FSR upscaling |
| `Super + Y` | Toggle NIS upscaling |
| `Super + I` | Increase FSR sharpness by 1 |
| `Super + O` | Decrease FSR sharpness by 1 |
| `Super + S` | Take a screenshot |
| `Super + G` | Toggle keyboard grab | 


# Sources
[https://docs.fedoraproject.org/en-US/gaming/gamescope/](fedoraproject.org)
* gamescope help text
* Copilot CLI was used to generate tables from `gamescope --help` command
