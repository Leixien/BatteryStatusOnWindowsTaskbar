# Linux (experimental)

A Linux build sits alongside the Windows app. It uses the same vendor drivers with a hidraw-based
HID backend and a GTK4 StatusNotifierItem tray icon; the Windows code path is unchanged.
All Linux-only files are in `linux/` and `src/linux/`, and `build-linux.sh` builds it (Windows keeps using `build.bat`).

| | Fedora | Ubuntu / Debian |
|---|---|---|
| Compiler & make | `sudo dnf install gcc-c++ make` | `sudo apt install g++ make` |
| GTK4 + Cairo | `sudo dnf install gtk4-devel cairo-devel` | `sudo apt install libgtk-4-dev libcairo2-dev` |

No extra HID library is needed (hidraw is used directly).

```sh
./build-linux.sh
./build-linux.sh test         # unit test for the HID report-descriptor parser
./wireless-battery --list     # print detected levels and exit
./wireless-battery --dump     # list HID collections
./wireless-battery --quit     # close the running tray instance
```

HID access needs a udev rule, otherwise the app starts but finds no devices:

```sh
sudo cp linux/99-wireless-battery.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && sudo udevadm trigger
# log out and back in
```

The tray icon works natively on KDE Plasma; GNOME needs an AppIndicator host such as
`gnome-shell-extension-appindicator`. The optional launcher is `linux/wireless-battery.desktop`
(install it plus `linux/wireless-battery.svg` and the binary into `~/.local/`).

Phase 1 covers Logitech, Razer, SteelSeries, Corsair, HyperX, PlayStation, Cooler Master, Glorious,
Finalmouse and the shared Kysona/Pulsar/ATK/G-Wolves protocols. Bluetooth/UPower fallbacks, HeadsetControl and
the remaining vendors are planned follow-up phases.
