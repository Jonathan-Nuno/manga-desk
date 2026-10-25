# Manga desk

> **Not released yet.** Manga desk 1.0 is in final testing. The downloads will appear on the [releases page](https://github.com/Jonathan-Nuno/manga-desk/releases) when it is published.

Manga desk is a free desktop app for macOS and Windows. It downloads chapters from websites that you set up, turns them into `.cbz` comic archives on your own disk, and copies them over a cable to an iPhone reader app. It works with readers that support file sharing, for example Inkshelf.

This repository holds the downloads, the user guide and the legal texts. The source code is not public.

## The content stance

Manga desk ships no content and no list of websites, and you should only add sources and download material you have the right to copy. By default it follows each site's robots.txt, paces its requests, and does not log in, get past paywalls or handle DRM.

## Download

Get the latest version from the releases page: `https://github.com/Jonathan-Nuno/manga-desk/releases/latest`.

| Computer | File to download |
| --- | --- |
| Mac with Apple silicon (M1 or newer) | `Manga-desk_<version>_aarch64.dmg` |
| Mac with an Intel processor | `Manga-desk_<version>_x86_64.dmg` |
| Windows 10 or 11, 64-bit (beta) | `Manga-desk_<version>_x64-setup.exe` |

Download only from this page. The macOS builds are signed and notarized by Apple. The Windows build is an unsigned beta, so Windows shows a SmartScreen warning; the install guide explains it.

The app also updates itself. See the user guide for how.

## System requirements

- macOS 13.5 (Ventura) or later, Apple silicon or Intel.
- Windows 10 or 11, 64-bit. No administrator rights are needed. Windows on ARM runs the app through emulation.
- About 100 to 120 MB of disk space for the app, plus room for your library.
- For the iPhone: a USB cable and a reader app with file sharing. On Windows, Apple's Apple Devices app from the Microsoft Store.

## Read first

- [User guide](docs/user/README.md)
- [Install on macOS](docs/user/install-macos.md)
- [Install on Windows](docs/user/install-windows.md)
- [Terms](docs/legal/terms.md)
- [Privacy](docs/legal/privacy.md)

## Report a problem

Open an issue in this repository. Say which version you use, which system you run, and what you did and saw. In the app, Settings › About › Copy diagnostics copies useful details to paste into the issue. It leaves out website addresses and source selectors, but read it before you paste it. Do not post private information.

## Affiliation

Manga desk is not affiliated with any website, with Apple or with Microsoft.
