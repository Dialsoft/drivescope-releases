# DriveScope

Drive tester for Windows by Dialsoft LLC (theITguy.com). Tests SSDs, hard drives and USB flash drives – health (S.M.A.R.T.), speed benchmarks, fake-capacity check, secure erase, partition tools, which operating system is on the drive – and prints test labels on a Brother QL label printer for resale.

## Download

Current version: **1.19.0** · Windows 10 or 11, 64-bit. Both downloads are the same program; pick one:

| | |
|---|---|
| **[⬇ Installer – DriveScope-Setup.exe](https://github.com/Dialsoft/drivescope-releases/raw/main/DriveScope-Setup.exe)** (recommended) | Installs just for you (no administrator password needed to install), adds Start menu and Desktop shortcuts and an uninstaller. Settings go in `%AppData%\DriveScope`, test reports in `Documents\DriveScope Reports`. |
| **[⬇ Portable – DriveScope.exe](https://github.com/Dialsoft/drivescope-releases/raw/main/DriveScope.exe)** | No installation: save it in a folder you can write to (Desktop, `C:\Tools` or a USB stick – not Program Files) and double-click it. Settings and reports stay next to the file. |

- If Windows shows **“Windows protected your PC”**, click **More info → Run anyway**.
- DriveScope asks for administrator rights each time it starts, because it reads drives directly.
- It opens in your web browser and keeps running in the system tray (bottom-right of the taskbar).
- Checksums (SHA-256): [DriveScope.exe.sha256](DriveScope.exe.sha256) · [DriveScope-Setup.exe.sha256](DriveScope-Setup.exe.sha256)

## Manual & video

- **[User manual](USER-MANUAL.md)** – also on the web at [dialsoft.com/drivescope/manual](https://dialsoft.com/drivescope/manual/) and as a [printable PDF](https://dialsoft.com/drivescope/DriveScope-Manual.pdf).
- **[Explainer video (2½ min)](drivescope-explainer.mp4)** – also on [dialsoft.com/drivescope](https://dialsoft.com/drivescope/#video).
- Inside DriveScope, every button and setting has a tooltip, and the **📖 Manual** button opens the manual.

## Updates

DriveScope checks this page a few seconds after it starts and every 6 hours, and offers new versions with one click (or installs them automatically when idle, if you switch that on). Installed and portable copies both update themselves. Each update is verified against its published SHA-256 checksum before it installs, and never during a test or erase.

## What's new

See [CHANGELOG.md](CHANGELOG.md) for every version. Latest (1.19.0):

- New installer (`DriveScope-Setup.exe`) alongside the portable `DriveScope.exe`.
- 📖 Manual button in the header; a full user manual, printable PDF and explainer video.
- Fixed: on some window sizes the page needed scrolling sideways.

---
© Dialsoft LLC. Built with Claude. QR codes by QR Code Generator for JavaScript © Kazuhiko Arase (MIT license).
