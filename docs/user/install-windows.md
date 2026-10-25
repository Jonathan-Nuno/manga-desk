# Install on Windows (beta)

The Windows version is a beta. The installer is not signed yet, so Windows shows warnings that you will not see on a signed program. This page explains each one. If you are not comfortable with that, wait for a signed release.

## What you need

- Windows 10 or Windows 11, 64-bit (x64). A PC with an ARM processor runs the x64 app through Windows's built-in emulation; there is no native ARM build.
- No administrator rights. The app installs for your user account only, under `%LOCALAPPDATA%`.
- WebView2, which Windows 10 and 11 normally already have. If your PC does not, the installer downloads it from Microsoft, so be online during the install.
- For the iPhone: Apple's Apple Devices app and a USB cable. See [Set up your iPhone](./iphone.md).
- About 100 to 120 MB of disk space for the app, plus room for the manga you download.

## Download

1. Open the latest release page: `https://github.com/Jonathan-Nuno/manga-desk/releases/latest`.
2. Download the file that ends in `-setup.exe`.

Download only from the releases page. Do not use a copy someone sent you.

## Install

1. Double-click the `-setup.exe` file.
2. If Windows shows "Windows protected your PC", read the next section.
3. Follow the installer. It does not ask for an administrator password.
4. Start Manga desk from the Start menu.

## SmartScreen: "Windows protected your PC"

SmartScreen warns about files it has not seen often. An unsigned installer starts with no reputation, and every new version of Manga desk starts from zero again. So you will see the warning for each new release.

If you downloaded the file from the releases page and want to continue:

1. Click More info.
2. Click Run anyway.

If the file came from anywhere else, do not run it.

## Smart App Control

Some Windows 11 PCs have Smart App Control turned on. It blocks an unsigned file that has no reputation, and it offers no Run anyway button and no way to allow one app. If your PC shows this block, you have two choices:

- Wait for a signed release of Manga desk.
- Turn Smart App Control off yourself: Windows Security › App & browser control › Smart App Control settings. This lowers your PC's protection, and on many Windows 11 versions you cannot turn it back on without resetting Windows. Read Microsoft's page on Smart App Control before you decide.

Manga desk never changes this setting for you.

## Uninstall

1. Quit Manga desk.
2. Open Windows Settings › Apps, find Manga desk, and choose Uninstall.

Your library folder stays where it is: the app never deletes it. The app also keeps a small folder with its settings, your source profiles and the optional browser support. Settings › About shows where it is. Delete that folder yourself if you want everything gone.

## Next step

Open the app and follow [Getting started](./getting-started.md).

## Report a problem

Open an issue in the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Say which message you saw and your Windows version.
