<div align=center>

<img src="extras/banner.png" alt="Banner" width="40%">

</div>
<h1 align=center>Counter-Strike: Source — Nintendo Switch port</h1>

This is a wrapper/port of the Android version of Counter-Strike: Source v1.09 (nillerusr
Source engine port). It loads the original game's ARM64 libraries and runs them
as-is in a minimalist fake-Android environment.

### How to install

You're going to need:
* the **Source Engine `.apk`** ([HERE](https://arumoon.github.io/source-engine-download/)) —
  for the shared engine `.so` modules and the fonts
* the **Counter-Strike: Source game files** from a legally owned copy of the game
  (the `cstrike/`, `hl2/` and `platform/` folders from a Steam install)
* the **cstrike APK** — for CS:S's own `libclient.so` / `libserver.so` and
  `extras_dir.vpk` (this is the APK this port was built against)

Create `/switch/css_nx/` on your SD card and lay it out like this:

```
/switch/css_nx/
  css_nx.nro
  config.txt            <- auto-created on first run
  lib/                  <- all .so files from the Source Engine APK's lib/arm64-v8a/,
                           THEN overwrite libclient.so + libserver.so with the two
                           from the cstrike APK's lib/arm64-v8a/
  assets/extras_dir.vpk <- from the cstrike APK's assets/
  files/                <- the fonts from the Source Engine APK's assets/
                           (dejavusans.ttf, dejavusans-bold.ttf, DroidSansFallback.ttf,
                           LiberationMono-Regular.ttf, Itim-Regular.otf)
  cstrike/              <- CS:S game data (cstrike_pak_dir.vpk + _NNN.vpk parts,
                           gameinfo.txt, steam.inf, resource/, maps/, ...)
  hl2/                  <- the shared Source content CS:S mounts (hl2_*.vpk)
  platform/             <- shared platform content (platform_*.vpk)
```

### Notes

This will not work in applet/album mode — use a game override (hold R on a title)
or a forwarder. The Switch needs the full application memory pool.

**Networking:** real libnx BSD sockets are wired through,
so LAN and direct `connect <ip>` reach the wire. There's no DNS resolver, so join
by IP, the master-server browser will not populate. CS:S's bots work offline.

A `config.txt` is created next to the `.nro` on first run:
* `screen_width` / `screen_height` — passed as `-w`/`-h` when both set; `-1` lets
  the engine pick by dock state (1920×1080 docked, 1280×720 handheld)
* `args` — extra Source command line (e.g. `+map de_dust2`)
* `lang` — Source language name (default `english`)
* `show_fps` — `1` to overlay the FPS counter
* `gamepad` — `1` to enable joystick input (default `1`)
* `console` — `1` to enable the developer console (default `1`)

### How to build

You need devkitA64 plus the following pacman packages:
* `switch-sdl2`
* `switch-mesa`
* `switch-libdrm_nouveau`
* `switch-zlib`
* `switch-ffmpeg`

Run `make`

### Credits

* nillerusr for the Android Source engine port this wraps
* TheOfficialFloW & fgsfds for the so-loader lineage
* the hl2_nx port this is derived from

### Support

If you enjoy my work and want to support me :

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/D1D1P2MOG)

### Legal

This project has no affiliation with Valve Corporation. "Counter-Strike",
"Half-Life" and "Source" are trademarks of their respective owners. All Rights
Reserved.

No assets or program code from the original game or its Android port are included
in this project. We do not condone piracy in any way, shape or form and encourage
users to legally own the original game.

Unless specified otherwise, the source code provided in this repository is
licensed under the MIT License. Please see the accompanying LICENSE file.
