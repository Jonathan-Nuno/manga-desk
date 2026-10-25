# Manga desk privacy

Manga desk has no accounts, no telemetry and no analytics. The publisher does not receive your library, your sources, your phone or your logs. This page says what the app keeps on your computer, what it sends over the network, and what the "Copy diagnostics" button does.

This is a plain-language text. It describes how the app works. The terms are published next to it.

## What the app stores, and where

Everything is on your computer, your phone or the library folder you chose. None of it is uploaded by the app.

- Settings: your library folder, your chosen phone and reader app, your first-launch choices and the time you confirmed the welcome note, update-check times, and your browser-support choice. These are in the app's own data folder. Settings › About shows where it is.
- Source profiles: the sources you typed or imported, with their website names, host names and page selectors. They are in the app's data folder.
- Browser support: if you install it, the browser files are in a folder inside the app's data folder. Remove deletes them.
- Logs: the app keeps a log of each job in its own data folder, and while the app downloads, the downloader also writes log files in your library folder: one `scrape.log` per series and one summary file. They can contain website addresses and the names of series. The Jobs screen shows each job's output.
- Your library: the page images and the `.cbz` archives, in the library folder you chose (a `downloads` folder and a `library` folder).
- Your phone: the app copies the series folders into the reader app's Documents folder on the iPhone. See the user guide page "Set up your iPhone" for exactly what it writes there.
- Phone details: to show your phones, the app reads each connected phone's name, model and iOS version, and the list of apps that have file sharing. The name of the phone and the reader app you pick are kept in the settings.

The app does not read your other files, contacts, photos or messages, on the computer or on the phone.

## What goes over the network

The app contacts only these:

1. The websites you set up. The app requests chapter pages, images and each site's robots.txt from the source's own site, its subdomains and the image hosts you list. It never contacts local or private network addresses. Those sites see your IP address and the app's user agent, which names Manga desk and its version and links to the releases repository. The app does not pretend to be a browser. If you use a browser (browser support), it uses the same user agent.
2. The release host, for update checks. The app asks the releases repository's web address for the latest version at launch (at most once a day) and when you choose Check now. If you confirm an update, it downloads the update from there. The release host, which is GitHub, sees an ordinary web request, including your IP address, and handles it under its own privacy terms.
3. The browser download, only if you choose to install browser support. The app downloads a browser from Playwright's download servers (`cdn.playwright.dev`, and Microsoft's mirror `playwright.download.prss.microsoft.com` when the first one does not answer). Those servers see an ordinary web request.
4. Your phone, over the cable or on your local network. This does not go to the internet.

The Windows installer may also download Microsoft's WebView2 component from Microsoft at install time if your PC does not have it. That happens in the installer, not while the app runs.

Nothing else. The app sends no telemetry, usage statistics, crash reports or identifiers, and has no advertising.

## Diagnostics

Settings › About › Copy diagnostics copies a short text to your clipboard. It holds the app version, the runtime version, the tools version, the browser revision and the folders the app uses. It leaves out website addresses, source selectors, and all of a phone's ID except its last 4 characters. The app copies it only when you press the button, and it sends it nowhere: you paste it into a message yourself. Read it first. Folder paths can contain your user name.

## Removing your data

- Delete the library folder to remove your downloads and archives.
- Delete series folders on the iPhone in the reader app or in Finder or the Apple Devices app.
- Uninstall the app, then delete the app's data folder (Settings › About shows it before you uninstall) to remove your settings, sources and browser support.

## Changes

If this text changes, the new text is published with the release that changes the behaviour.

## Contact

Contact the publisher through the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Do not post private information there.
