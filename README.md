# Manga desk

Manga desk is a free desktop app for macOS. It downloads chapters from websites that you set up, turns them into `.cbz` comic archives on your own disk, and copies them over a cable to an iPhone reader app. It works with readers that support file sharing, for example [Inkshelf: Manga & Comic Reader](https://apps.apple.com/us/app/inkshelf-manga-comic-reader/id6824132149) from the App Store.

This repository holds the downloads, the user guide and the legal texts. The source code is not public.

## The content stance

Manga desk ships no content and no list of websites, and you should only add sources and download material you have the right to copy. By default it follows each site's robots.txt, paces its requests, and does not log in, get past paywalls or handle DRM.

## Download

Get the latest version from the releases page: `https://github.com/Jonathan-Nuno/manga-desk/releases/latest`.

| Computer | File to download |
| --- | --- |
| Mac with Apple silicon (M1 or newer) | `Manga-desk_<version>_aarch64.dmg` |
| Mac with an Intel processor | `Manga-desk_<version>_x86_64.dmg` |

Download only from this page. Both builds are signed by their publisher and checked by Apple (notarized). Manga desk is not available for Windows.

The app also updates itself. See the user guide for how.

## System requirements

- macOS 13.5 (Ventura) or later, Apple silicon or Intel.
- About 250 MB of disk space for the app, plus room for your library.
- For the iPhone: a USB cable and a reader app with file sharing, such as Inkshelf.

## Read first

- [User guide](docs/user/README.md)
- [Install on macOS](docs/user/install-macos.md)
- [Terms](docs/legal/terms.md)
- [Privacy](docs/legal/privacy.md)

## Report a problem

Open an issue in this repository. Say which version you use, which system you run, and what you did and saw. In the app, Settings › About › Copy diagnostics copies useful details to paste into the issue. It leaves out website addresses and source selectors, but read it before you paste it. Do not post private information.

## Affiliation

Manga desk is not affiliated with any website or with Apple.
