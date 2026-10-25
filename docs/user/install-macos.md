# Install on macOS

## What you need

- macOS 13.5 (Ventura) or later.
- A Mac with Apple silicon (M1 or newer) or an Intel processor. There is one download for each.
- About 100 to 120 MB of disk space for the app, plus room for the manga you download.
- An internet connection for the download and for the sources you set up.

## Download the right file

1. Open the latest release page: `https://github.com/Jonathan-Nuno/manga-desk/releases/latest`.
2. Find out which Mac you have. Choose the Apple menu › About This Mac. If the line says Chip followed by Apple M1, M2 or similar, you have Apple silicon. If it says Processor followed by Intel, you have an Intel Mac.
3. Download the `.dmg` that matches:
   - Apple silicon: the file whose name contains `aarch64`.
   - Intel: the file whose name contains `x86_64`.

Download only from the releases page. Do not use a copy someone sent you.

## Install

1. Double-click the `.dmg`. A small window opens with Manga desk on the left, the Applications folder on the right and an arrow between them. It says "Drag Manga desk to Applications".
2. Drag Manga desk onto the Applications folder in that window.
3. Open Manga desk from Applications (in Finder, choose Go › Applications).

The first time you open it, macOS asks you to confirm that you want to open an app downloaded from the internet. This is normal. Click Open.

### Eject the installer

While the installer disk is still open, Manga desk shows a line under its top bar: "Manga desk is installed." Click **Eject installer**. The disk is ejected and its window closes. Click **Not now** to keep it open; the line comes back the next time you open the app while the disk is still there.

If the disk does not eject (for example because a Finder window is still showing something on it), the app says so. Close that window, then eject "Manga desk" in the Finder sidebar, or Control-click the disk on the desktop and choose Eject. You can delete the `.dmg` file afterwards.

If you opened Manga desk straight from the installer window instead, the line says "Manga desk is running from the installer disk." Drag Manga desk to Applications in the installer window, quit the copy that is running, then open Manga desk from Applications.

The app is signed by its publisher and checked by Apple (notarized). Nothing more is needed.

## If macOS shows a different message

macOS has two messages that look alike and mean different things. Read yours before you do anything.

### "Apple cannot check it for malicious software"

A release from the releases page should not show this message. It can appear if the file was not the official one, or if the download was cut short.

1. Download the file again from the releases page and try again.
2. If you are sure you have the official file and macOS still blocks it, you can allow it once. Open System Settings › Privacy & Security, scroll to the Security section, click Open Anyway next to the app's name, confirm, and enter your password. The Open Anyway button is there for about an hour after you tried to open the app.
3. Report the problem (see the end of this page).

### "Manga desk is damaged and can't be opened"

Do not override this message. It means the signature does not match the file.

1. Move the app (or the `.dmg`) to the Trash.
2. Download it again from the releases page.
3. If the message comes back, report the problem. Do not try to get around it with a Terminal command or a setting.

## Uninstall

1. Quit Manga desk.
2. Drag Manga desk from Applications to the Trash.

Your library folder stays where it is: the app never deletes it. The app also keeps a small folder with its settings, your source profiles and the optional browser support. Settings › About shows where it is. Delete that folder yourself if you want everything gone.

## Next step

Open the app and follow [Getting started](./getting-started.md).

## Report a problem

Open an issue in the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Say which message you saw, your macOS version and whether your Mac is Apple silicon or Intel.
