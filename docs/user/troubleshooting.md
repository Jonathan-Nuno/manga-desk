# Troubleshooting

Find the message or symptom you see. Each section says what it means and what to do.

Install problems:

- [macOS says it cannot check the app, or that it is damaged](#macos-gatekeeper)
- [Windows shows "Windows protected your PC"](#windows-smartscreen)
- [Windows blocks the installer with no way to continue](#windows-smart-app-control)

iPhone problems:

- [The app cannot find the iPhone](#the-app-cannot-find-the-iphone)
- [The iPhone has not trusted this computer](#the-iphone-has-not-trusted-this-computer)
- [The iPhone is locked](#the-iphone-is-locked)
- [The Apple device service is missing](#the-apple-device-service-is-missing)
- [The reader app is not in the list](#the-reader-app-is-not-in-the-list)
- [The sync says files differ or are missing](#the-sync-says-files-differ-or-are-missing)

Download problems:

- [robots.txt disallows a page](#robotstxt-disallows-a-page)
- [The site asks for a long Crawl-delay](#the-site-asks-for-a-long-crawl-delay)
- [The site is rate limiting](#the-site-is-rate-limiting)
- [Browser support is not installed](#browser-support-is-not-installed)
- [No source profile for a host](#no-source-profile-for-a-host)
- [A host is refused](#a-host-is-refused)
- [No page images found](#no-page-images-found)
- [Images fail in a row](#images-fail-in-a-row)

Finding information:

- [Where the logs are](#where-the-logs-are)
- [Copy diagnostics](#copy-diagnostics)

## macOS Gatekeeper

macOS shows one of two messages that mean different things. "Apple cannot check it for malicious software" should not appear for a release from the releases page. "Manga desk is damaged and can't be opened" is never to be overridden. Both are explained step by step in [Install on macOS](./install-macos.md).

## Windows SmartScreen

"Windows protected your PC" appears for the unsigned beta installer, once for every new version. If the file came from the releases page, choose More info, then Run anyway. See [Install on Windows](./install-windows.md).

## Windows Smart App Control

With Smart App Control on, Windows 11 blocks the unsigned installer and offers no Run anyway. See [Install on Windows](./install-windows.md) for the two choices.

## The app cannot find the iPhone

The message reads like "No iPhone <name> is connected". Check these in order:

1. The cable is plugged into the computer and the iPhone, and the cable carries data (some cables only charge).
2. The iPhone is unlocked.
3. On the iPhone you tapped Trust (see the next sections).
4. On macOS, Finder shows the iPhone in its sidebar. On Windows, the Apple Devices app shows it.
5. Refresh the list in Settings › iPhone.

If you use Wi-Fi sync, the phone must be on the same network with Wi-Fi sync turned on in Finder or the Apple Devices app. Wi-Fi is best effort, and the cable is more reliable. On Windows the cable is required.

## The iPhone has not trusted this computer

The message reads "The iPhone <name> has not trusted this computer yet. Unlock the iPhone, connect it to this computer, open Finder (macOS) or the Apple Devices app (Windows) and tap Trust."

1. Unlock the iPhone and connect it with the cable.
2. Open Finder (macOS) or the Apple Devices app (Windows).
3. Tap Trust on the iPhone and enter its passcode.
4. Try again.

If the question does not appear, unplug the cable, plug it in again, and unlock the phone.

## The iPhone is locked

The message reads "The iPhone <name> is locked. Unlock it, keep it unlocked while it syncs, and try again." Unlock the iPhone, keep it unlocked until the sync ends, and start the sync again. Finished files are not copied again.

## The Apple device service is missing

The message reads "Cannot reach the Apple device service (usbmuxd)." followed by a hint.

- macOS: the service is part of macOS. Connect the iPhone with a cable, open Finder once so that it shows the iPhone, then try again.
- Windows: install the Apple Devices app from the Microsoft Store, open it once with the iPhone connected, then try again. iTunes also provides the service. Manga desk shows a link to the Microsoft Store page.

## The reader app is not in the list

The list shows only the apps on the iPhone that have file sharing turned on. If the app you want is missing:

1. Check that the iPhone is connected, unlocked and trusting this computer.
2. Check that the app is installed on this iPhone.
3. Refresh the list.

If the app is installed and still missing, it does not support file sharing. You cannot turn file sharing on yourself: it is set by the app's developer. Use a reader that supports it, or copy files by hand (see [Set up your iPhone](./iphone.md)).

The message may read "<app> on the iPhone does not share its Documents folder (file sharing is off), so files cannot be copied into it" or "<app> is not installed on the iPhone". Choose another reader in Settings › iPhone.

## The sync says files differ or are missing

After copying a series, the app lists the folder on the phone again and checks every file. If a file is missing or has a different size, the sync names the file and reports a problem.

1. Run the sync again. It copies only the files that are missing or different.
2. Keep the cable connected and the iPhone unlocked for the whole sync.
3. Make sure the iPhone has free storage.
4. If the same files fail again, report it with the diagnostics (see below).

Extra files on the phone that are not in your library are listed as extra and left alone. They are not a problem.

## robots.txt disallows a page

The message reads "robots.txt disallows <address>; stopping." The site's robots.txt asks automated tools not to fetch that page, so the app stopped and fetched nothing from it. Test shows the verdict as disallowed.

- Check that the chapter address and the source's hosts are correct.
- Use a site that allows it, or ask the site's owner.
- Turning off Respect robots.txt for the source is your decision and your responsibility. See [Sources](./sources.md).

A message like "Cannot check <robots.txt address>: HTTP <number>; stopping." means robots.txt exists but the site answered with an error. Try again later.

## The site asks for a long Crawl-delay

The message reads "robots.txt asks for Crawl-delay <number>s at <host>, over 60s; stopping." The site asks for more than a minute between requests. The app never shortens a requested delay and stops instead. A shorter Crawl-delay is not an error: the app just waits that long between requests.

## The site is rate limiting

You see "Rate limited (HTTP 429)" or "(HTTP 503)" followed by "waiting 60s (1/5)". The site is asking the app to slow down. The app waits, then continues. The wait doubles each time, up to 15 minutes.

The run stops after five waits, or if the site asks for a wait over 15 minutes ("server asks for <number> min, rerun later"). Run it again later, for example in an hour. Chapters that finished are skipped and the run picks up where it stopped.

## Browser support is not installed

The message starts "Browser support is not installed". The page needs a browser and none is set up. Open Settings › Browser support and install it or choose Chrome or Edge. See [Browser support](./browser-support.md). If a source works as HTML, set its render mode to HTML.

## No source profile for a host

The message reads "No source profile for <host>". The address you pasted has a host that no source covers, so the app stopped before it made any request.

1. Open Sources in the top bar.
2. Add or import a source whose Hosts include that host or its parent. For `www.example.org`, a source for `example.org` is enough.
3. Try again.

When several series are downloaded together, the series with the missing source fails and the others still run.

## A host is refused

The message reads "Refused <host>: not the start site; add it to ALLOWED_HOSTS if it is the site's image host". The page points at a host that is not the source's site, its subdomains or one of its image hosts. If it is the site's image host, add it to Image hosts in the source. The log message calls this setting ALLOWED_HOSTS. Do not add a host you do not know.

A message like "Refused <host>: resolves to <address>" means the address is on a private or local network. The app never contacts those, on purpose.

## No page images found

The message reads "No page images found; check PAGE_CONTAINER and PAGE_IMAGE." The page container or page image selector found nothing. Use Test on the chapter address and change the selectors. If the page lists its images with JavaScript, set the render mode to Auto or Browser and set up [browser support](./browser-support.md).

## Images fail in a row

The message reads "<number> images failed in a row; rerun later to resume." The site stopped serving images, the address changed, or the network dropped. Rerun later. A run keeps what it has and picks up from there.

## Where the logs are

- The Jobs screen shows the output of each job. The app also keeps each job's log in its own data folder, which Settings › About shows.
- The downloader also writes a log file for every series, `downloads/<series>/scrape.log`, and a one-line summary per run in `downloads/scrape.log`. Both are inside your library folder. Settings › Library folder shows where it is.

Log files can contain website addresses. Read them before you share them.

## Copy diagnostics

Open Settings › About and choose Copy diagnostics. The app copies a short text to your clipboard. It lists the app version, the runtime version, the tools version, the browser revision and the folders the app uses. It leaves out website addresses, source selectors and all but the last 4 characters of a phone's ID. Nothing is sent anywhere: you paste it into your problem report yourself.

Read the text before you paste it. Folder paths can contain your user name.
