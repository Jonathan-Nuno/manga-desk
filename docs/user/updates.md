# Updates

Manga desk can update itself, and you can always update by hand.

## Automatic update check

- Manga desk checks for a new version when it starts, at most once a day.
- Open Settings › Updates to see the current channel, the time of the last check and a Check now button. There is one channel, stable.
- If the app cannot reach the update server, for example without an internet connection, Settings › Updates says "could not check" and shows when it last tried. Check now tries again.
- If a new version exists, the app shows its version and its release notes. Nothing is installed until you choose Install and relaunch.
- The app installs an update only when no download, conversion or sync is running. Wait for the job to finish, or stop it.
- After the update the app restarts.

Updates are signed. The app installs only an update whose signature matches the key built into it.

Your library, your settings and your sources stay as they are.

## Update by hand

1. Open the latest release page: `https://github.com/Jonathan-Nuno/manga-desk/releases/latest`.
2. Download the file for your computer, as described in [Install on macOS](./install-macos.md) or [Install on Windows](./install-windows.md).
3. Install it over the old version. On macOS, drag Manga desk to Applications and choose Replace. On Windows, run the setup file again.

On Windows, a new version of the unsigned beta can show the SmartScreen warning again. See [Install on Windows](./install-windows.md).

## If a check fails

If the check cannot reach the release server, you are probably offline or the site is down. Try again later. Manga desk keeps working without it.

## What the check sends

The check is an ordinary web request to the release host. It sends nothing from your library, your sources or your phone. See [Privacy](../legal/privacy.md).
