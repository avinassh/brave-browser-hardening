## [Linux specific Tips](#linux-specific-tips)

You can create a file called `chrome-flags.conf` and put it into `$HOME/.config/chrome-flags.conf`, this makes it easier to work with flags without opening the Browser.

Example `chrome-flags.conf` below:

```sh
-use-vulkan
--disable-features=UseChromeOSDirectVideoDecoder
--disable-gpu-driver-bug-workarounds
--enable-accelerated-2d-canvas
--enable-accelerated-video-decode
--enable-features=VaapiVideoDecoder
--enable-gpu-rasterization
--enable-oop-rasterization
--enable-zero-copy
--ignore-gpu-blocklist
# Borked until Chrome 96
#  https://chromiumdash.appspot.com/commit/a4de986102a45e29c3ef596f22704bdca244c26c
# ... and Chrome 98
# https://bugs.chromium.org/p/chromium/issues/detail?id=1236697
#
# Up to you and your preference and device.
# --gpu-testing-vendor-id=0x8086
# --gpu-testing-device-id=0x5917
# --force-device-scale-factor=1.00
# --enable-features=WebUIDarkMode
# --force-dark-mode
```

- You can enforce the usage of [vaapi](https://github.com/brave/brave-browser/issues/1024) by default via `brave --enable-oop-rasterization --enable-accelerated-video-decode`.
- To enforce [Wayland](https://github.com/brave/brave-browser/issues/6212) support (Chromium 87+) you can use `brave --enable-features=UseOzonePlatform --ozone-platform=wayland`.
- [SIGSEGV & SIGTRAP error codes in Brave](https://bbs.archlinux.org/viewtopic.php?pid=1950852#p1950852)
- No video hardware acceleration available on some pages: Some videos on e.g. YouTube are encoded using AV1 and Brave will use dav1d software decoder for that. But for ones encoded differently, Brave will indeed uses GPU for it if you enabled `--enable-features=VaapiVideoDecoder on`.
- `Override software rendering list` flag can be used to enforce that your GPU will be used (which might be blacklisted otherwise).
- `Enable Mojo Shared Memory Channel` flag can be used to share messages from GPU buffer, which might increase performance a bit.
- On Ubuntu based Distros I personally use the following combination for pass-through  `--ignore-gpu-blocklist`, `--enable-gpu-rasterization`, `--enable-zero-copy`, `--disable-gpu-driver-bug-workarounds` and `--use-gl=desktop`. Keep in mind that rasterization and zero-copy are highly unstable (depends on the OS/distro).
- [Font rendering can be a PITA](https://lonesysadmin.net/2011/09/12/how-to-fix-google-chrome-font-rendering-issues/), Settings --> Advanced --> System --> Hardware Acceleration is your first starter here.
- `#enable-gpu-rasterization` + `#enable-zero-copy` + `#canvas-oop-rasterization` combined can boost the performance on Linux by solid 10 percent, do not enable those flags on other platforms.

