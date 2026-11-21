# Features

## Display

**On the taskbar (default):** `🎧 30%  🖱 93%` next to the notification area, drawn with the Windows icon font.
- **Low battery:** a red number means 15% or less.
- **Charging:** a blue ⚡ appears next to the number. Once the device is fully charged and still on power, it turns into a green ✓.
- **Asleep:** dimmed text means the device is asleep and the last known value is shown. Turn off *Dim sleeping devices* in the menu to keep that value at full brightness.
- **Disconnected (optional):** turn on *Show disconnected devices* to display a dimmed `×` for devices whose driver explicitly reports an offline wireless link. This does not infer disconnection from a missed battery poll; the default remains to hide offline devices.
- **Two devices of one kind:** with two mice (or two controllers...) both would get the same icon, so each one gets a tiny caption of up to 3 letters in the corner of its icon, taken from its name (`MX`, `PRO`), or a number when the names do not tell them apart. A device that is alone in its kind shows no caption.
- **Theme:** it follows light/dark mode and DPI scaling.
- **Transparent taskbar themes** (e.g. Windhawk's Taskbar Styler): turn on *Background behind taskbar text* in the menu to keep the text readable over the wallpaper.
- **Several monitors:** the widget shows on every monitor's taskbar, next to its clock, so it stays visible while a game runs fullscreen. *Show the widget on* in the menu picks *All monitors*, *Main monitor only*, or one display (e.g. only *Display 3*).
- **More display options:** *Icons above percentages* stacks each icon over its level to save width; *Brand colors* shows known brands in their color (Razer green, HyperX red, ...) with a small level bar; two devices of the same kind get a tiny caption so they can be told apart; left and right taskbars get a column of devices.
- **Languages:** English, العربية, Deutsch, Español, فارسی, Français, עברית, 日本語, 한국어, Magyar, Polski, Português (Brasil), Русский, Svenska, Tiếng Việt, Türkçe, Українська, 简体中文 and 繁體中文. The app follows the Windows display language; *Language* in the menu picks another one. See [Translations](translations.md) to add or improve a language.
- **Brand colors:** devices of 15 known brands get their maker's color, with a soft glow and a thin level bar under the
  percentage: Razer green, Logitech blue, SteelSeries orange, Corsair yellow, HyperX / ROG / ZOWIE red, PlayStation,
  Xbox, Samsung, Apple, Jabra, JBL, Cooler Master and Steam. Each color has a dark- and a light-taskbar shade. The brand
  comes from the driver that found the device, then the vendor ID, then the name; colors and rules are in
  `src/brands.cpp`. Turn it off with *Brand colors* in the menu.

**Tray icons:** one icon per device with the number drawn in it, plus a "Low battery" notification at 15%. The app switches to this automatically when the taskbar is vertical or can't be found.

**Custom device names:** open the device submenu and select *Rename device...* to set a name
(up to 64 characters). The name is shown in the taskbar widget's tooltip/caption,
tray tooltip and notifications, and the device menu. Use *Reset to original name*
to restore the driver's name. Names are stored locally in the current user's
Windows registry (`Software\WirelessBattery`, `DeviceAliases`), using the stable
device key. Renaming never changes driver matching, protocol queries, or `--list` /
`--dump` diagnostic output. No account or network access is needed.

Hover for details. Click for the menu: every device (click one to hide or show it), display mode, *Refresh now*, *Start with Windows*, and *Exit*. Levels refresh every 60 seconds (*Check battery every* in the menu changes this), and right away when a device is plugged in or the PC wakes up.

## Smart Battery Alerts (experimental)

You can set a **per-device low-battery notification threshold** from each device's
submenu: **Battery alerts** → *Use default (15%)*, *Disable notifications*,
or one of 5%, 10%, 15%, 20%, 25%, 30%, 35%, 40%. The existing 15% default stays
unchanged unless you choose an override. Settings are stored by device key in
the current user's Windows registry (`Software\WirelessBattery`, `AlertThresholds`).

An alert is triggered only from a real, fresh 0–100% battery reading when the
device is connected, awake and not charging. An alert is issued once, and will
re-arm after the level climbs more than 10 percentage points above the chosen
threshold (or when charging begins). Missing readings or sleeping devices do
not retrigger alerts. Hidden devices don't produce notifications. Disabling
notifications for one device does not hide it or change its percentage.

Both taskbar-widget and tray-icon modes support notifications. Since Windows
needs a notification-area icon to display a legacy balloon, widget mode may
show a temporary notification icon for up to one minute after an alert.
Widget colours and the low-battery highlight still use the project's
original global 15% threshold, independently of the notification setting.

## Battery history & insights

Right-click a device in the taskbar widget or tray menu and choose **Battery history...**.
The native, DPI-aware viewer (it follows the Windows light/dark theme) shows recorded battery levels with connected sample lines over the last **24 hours**, **7 days**, or **30 days**, along with the latest reading, lowest/highest level, change in percentage points, and sample count. You can clear the selected device's history from the viewer.

History is recorded **locally only** for connected, awake devices reporting a numeric percentage. Readings are sampled at most once every 30 minutes per device (except charging-state transitions, with a 60-second minimum). Data is kept for up to 30 days and the local file is kept under about 2 MB. The app never probes hardware beyond its existing polling, sends no history data over the network, and makes a conservative, approximate time-to-empty estimate from recent discharge observations only. At least four points, two hours, a three-percentage-point decline, a fresh reading and a stable discharge segment are required. Charging, old readings or insufficient data suppress the estimate; device-reported runtime is not available. The estimate is not a guarantee. Missing chart data is shown as gaps, not interpolated.

Turn off **Record battery history** in the menu to stop saving readings; what was already saved stays until you clear it in the viewer. The file is stored in `%LOCALAPPDATA%\WirelessBattery\battery_history.tsv`. Its device identities are encoded (not encrypted); the file is local to your Windows account. In `--demo`, the chart uses synthetic data that is never saved. **Note:** history starts collecting only after this feature is installed and the app has been running for a while.

## Updates on Windows

Official stable Windows builds check the project's latest published stable release in the
background, 30 seconds after startup and then every 24 hours while the app is running. Open the
menu to see **Update available: vX.Y.Z...**, or choose **Check for updates...** yourself.
Update information appears only in this menu: battery icons, percentages and tooltips stay the
same, and automatic checks never show a notification or dialog. Turn off
**Automatically check for updates** in the menu to disable background checks.

For an installed copy, click the update entry and **Download and install**. Nothing is installed
without that click. The app downloads the release's `SHA256SUMS.txt` and its signature, checks the
signature against the maintainer's public key built into the app, downloads the Windows installer,
and runs it only if its SHA-256 is the one in the signed list (and the one GitHub lists for it). It
then updates the existing installation. Settings and startup preference are
preserved, and the app reopens after installation. An installation for all users can ask for
administrator permission. **Release notes** opens the official release page; **Later** keeps
your current version. Portable copies offer the release page for downloading the ZIP manually.

Checks contact GitHub's public API without an account or token. No device or battery information
is sent. Offline failures and GitHub rate limits leave battery monitoring running; a previously
found release stays in the menu until a successful check supersedes it or it is installed.
Cancelling a download waits for the current network operation to finish its finite timeout.
The installer never restarts Windows automatically.

**Why updates are safe to install:** the signing key never goes to GitHub. The maintainer signs
each release's checksum list on their own PC (see [docs/releasing.md](releasing.md)), so
even someone who took over the GitHub account or its build workflow could not publish an update
the app would install. A release without a valid signature is shown in the menu but can only be
downloaded by hand. The signature does not replace Windows' own SmartScreen or UAC prompts.

Install the first release containing this feature manually once. Development/test builds disable
official update checks so local changes cannot be replaced accidentally. Updates for Linux and
automatic replacement of portable copies are deferred.

## How it works

Each vendor driver in [`src/drivers/`](../src/drivers) recognises its devices by USB vendor and product ID, and only ever sends read-only battery queries. Unknown devices are never written to. The generic fallbacks (HID battery usage, Bluetooth, XInput, HeadsetControl) only look at devices no vendor driver has claimed.

The taskbar widget is a layered child window of `Shell_TrayWnd`, placed left of `TrayNotifyWnd`. If Explorer restarts, it is re-created.
