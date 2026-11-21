# BatteryHub

Battery levels of your wireless mouse, headset, keyboard and controller, right on the Windows taskbar.

![BatteryHub on the taskbar](docs/screenshot.png)

[![Latest version](https://img.shields.io/github/v/release/krisgfx9/Wireless-Device-Battery-Monitor?label=latest&style=flat)](https://github.com/krisgfx9/Wireless-Device-Battery-Monitor/releases/latest)
[![Discord](https://img.shields.io/badge/Discord-Join%20us-5865F2?logo=discord&logoColor=white)](https://discord.gg/ZgDDUPP8ye)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20me-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/krisgfx)

*Formerly **Wireless Battery**; updating keeps your settings, startup choice and battery history.*

- **Tiny:** ~350 KB, ~2 MB of RAM, plain C++/Win32, no runtime or background service.
- **No vendor apps needed** for most devices: drivers send read-only battery queries directly.
- **Many brands:** Logitech, Razer, SteelSeries, Corsair, HyperX, Glorious, Jabra, JBL, PlayStation, Xbox, Samsung Galaxy Buds, AirPods, any Bluetooth device with a battery level, and every headset [HeadsetControl](https://github.com/Sapd/HeadsetControl) supports. → [Full device list](docs/devices.md)
- **Taskbar widget or tray icons**, low-battery alerts, charging/asleep indicators, battery history, light/dark theme, multi-monitor, 19 languages. → [All features](docs/features.md)

## Install

Download **`BatteryHub-Setup-<version>.exe`** from the [latest release](https://github.com/krisgfx9/Wireless-Device-Battery-Monitor/releases/latest) and run it. The per-user install needs no administrator rights. Prefer no installer? Use the portable zip.

The exe is not code-signed, so SmartScreen may warn: click *More info → Run anyway*. On Windows 11, tray icons may land in the `^` overflow; drag them onto the taskbar.

## Command line

```
BatteryHub.exe --list     # print every device and its battery level, then exit
BatteryHub.exe --json     # same, as a JSON array
BatteryHub.exe --dump     # all HID/USB/Bluetooth devices (also saved to %TEMP%\BatteryHub-dump.txt)
BatteryHub.exe --report   # open the "Request support for a device" window
BatteryHub.exe --demo     # sample devices instead of real ones
BatteryHub.exe --quit     # close the running instance
```

**Device not shown?** Right-click the widget and choose **Request support for a device...**, or [open an issue](https://github.com/krisgfx9/Wireless-Device-Battery-Monitor/issues/new) with the `--dump` output.

## Build

Needs [MinGW-w64](https://www.mingw-w64.org/) (e.g. MSYS2: `pacman -S mingw-w64-x86_64-gcc make`) and PowerShell.

```
make                                  # development build
build.bat                             # same, from cmd with g++ and windres on PATH
make test VERSION=1.2.3 CHANNEL=test  # regression tests
```

The installer is built with [Inno Setup](https://jrsoftware.org/isinfo.php): `powershell -File installer\build-installer.ps1 -Version 1.2.3` (see [docs/releasing.md](docs/releasing.md)). A [Linux build](docs/linux.md) is experimental.

## More

[Supported devices & limitations](docs/devices.md) · [Features](docs/features.md) · [Translations](docs/translations.md) · [Contributing](CONTRIBUTING.md) · [Credits](docs/credits.md)

## License

[GPL-3.0-or-later](LICENSE).
