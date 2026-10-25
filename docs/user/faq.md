# FAQ

## Does Manga desk include manga or a list of sites?

No. It ships no content, no catalog, no search and no list of websites. You paste addresses and set up the sources yourself.

## Is it free?

Yes. Manga desk is free to use and its source code is not public. The [Terms](../legal/terms.md) say what you may do with it.

## Which sites does it work with?

That depends on the sources you set up. The app does not provide or recommend any. See [Sources](./sources.md).

## Is it legal to download from a site?

That depends on the material, the site's terms and the laws where you live. Manga desk cannot tell you, and nothing in this guide is legal advice. Only download material you have the right to copy. You are responsible for what you add and download.

## Why is it slow?

On purpose. The app downloads one page at a time, waits between pages and chapters, follows the site's robots.txt and backs off when a site asks it to. See [Sources](./sources.md).

## Can it log in to a site, or download paid or protected chapters?

No. It does not log in, keep cookies, get past paywalls or handle DRM, and support for these will not be added.

## Do I need an iPhone?

No. Without a phone, the `library` folder holds `.cbz` files that any comic reader that opens `.cbz` can use. See [Set up your iPhone](./iphone.md) for ways to copy them.

## Which reader apps work?

Readers on the iPhone that support file sharing, for example Inkshelf. Only apps with file sharing appear in the list in Settings › iPhone.

## Does it work with Wi-Fi?

The cable is the supported way. On macOS, Wi-Fi sync can work when the phone is on the same network and Wi-Fi sync is on in Finder, but it is best effort. On Windows the cable is required.

## Does the sync delete anything on my phone?

No, apart from its own leftover temporary files from an interrupted copy. See [Set up your iPhone](./iphone.md).

## Where are my files?

In your library folder (Settings › Library folder shows it). `downloads` holds page images and `library` holds the `.cbz` archives. The app's own settings and source profiles are in a separate folder that Settings › About shows.

## How do I free up disk space?

Open Storage. Once a chapter has an archive in `library`, Prune can remove its original page images. Pruned chapters are still treated as done. You can also delete a series folder yourself.

## Does Manga desk collect data about me?

No. It has no telemetry, analytics or accounts. See [Privacy](../legal/privacy.md) for exactly what goes over the network.

## Can I use it on Linux, Android or iPad?

No. There are builds for macOS and Windows.

## How do I update it?

The app checks once a day and asks before it installs. See [Updates](./updates.md).

## How do I uninstall it?

See [Install on macOS](./install-macos.md) or [Install on Windows](./install-windows.md). Your library folder is never deleted by the app.

## How do I report a problem?

Open an issue in the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Add the text from Settings › About › Copy diagnostics, and say what you did and what you saw.
