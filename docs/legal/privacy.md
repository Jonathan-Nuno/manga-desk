# Manga desk privacy

Manga desk has no accounts, no telemetry and no analytics. The publisher does not receive your library, your sources, your phone or your logs. This page says what the app keeps on your computer, what it sends over the network, and what the "Copy diagnostics" button does.

This is a plain-language text. It describes how the app works. The terms are published next to it.

## What the app stores, and where

Everything is on your computer, your phone or the library folder you chose. None of it is uploaded by the app, except for what the optional source agent sends when you ask it to (item 4 under "What goes over the network").

- Settings: your library folder, your chosen phone and reader app, your first-launch choices and the time you confirmed the welcome note, update-check times, your browser-support choice and your source-agent model choice. These are in the app's own data folder. Settings › About shows where it is.
- Source profiles: the sources you typed or imported, with their website names, host names and page selectors. They are in the app's data folder.
- Browser support: if you install it, the browser files are in a folder inside the app's data folder. Remove deletes them.
- Logs: the app keeps one log of its own, `logs/manga-desk.log` in its data folder, with its start-up line, update messages and errors; it starts again at each launch. While the app downloads, the downloader also writes log files in your library folder: one `scrape.log` per series and one summary file. They can contain website addresses and the names of series. The Jobs screen shows each job's output while the app is open, including the selectors a source-agent job proposed and its notes but not the pages' HTML; job output is not saved to a file.
- Anthropic API key (optional): if you add one for the source agent, it is stored in your computer's credential store, the Keychain on a Mac or Credential Manager on Windows, under the name "Manga desk". It is not in the app's data folder, the settings, the logs or any other file. The app does not show it again. Settings › Agent › Remove deletes it.
- Source-agent spend: a file called `agent-usage.jsonl` in the app's data folder. For each model call of the source agent it holds the time, the model, the token counts, the estimated cost and the job's number. It holds no page content, no website address and no key. Settings › Agent adds up the current month from it.
- Your library: the page images and the `.cbz` archives, in the library folder you chose (a `downloads` folder and a `library` folder).
- Your phone: the app copies the series folders into the reader app's Documents folder on the iPhone. See the user guide page "Set up your iPhone" for exactly what it writes there.
- Phone details: to show your phones, the app reads each connected phone's name, model and iOS version, and the list of apps that have file sharing. The name of the phone and the reader app you pick are kept in the settings.

If you enable experimental saved browser sessions, `browser-sessions/` in the app's data folder holds a separate Chrome or Edge profile per source origin. It can contain cookies, local storage, browsing history and cache from the verification window. These stay on your computer and are not included in source exports or diagnostics. The app does not read your ordinary browser profile.

The app does not read your other files, contacts, photos or messages, on the computer or on the phone.

## What goes over the network

The app contacts only these:

1. The websites you set up. The app requests chapter pages, series pages, images and each site's robots.txt from the source's own site, its subdomains and the image hosts you list. When the source agent drafts a source, the app also checks the first page image of each chapter it tests and the series cover on the image hosts those pages name, reading only the start of each image. It never contacts local or private network addresses. Those sites see your IP address and the app's user agent, which names Manga desk and its version and links to the releases repository. The app does not pretend to be a browser. If you use the hidden browser (browser support), it uses the same user agent. Experimental saved browser sessions instead use the selected browser’s native user agent and cookies. Their verification window is a normal browser window and may contact additional sites loaded by that page, including its verification provider and browser services.
2. The release host, for update checks. The app asks the releases repository's web address for the latest version at launch (at most once a day) and when you choose Check now. If you confirm an update, it downloads the update from there. The release host, which is GitHub, sees an ordinary web request, including your IP address, and handles it under its own privacy terms.
3. The browser download, only if you choose to install browser support. The app downloads a browser from Playwright's download servers (`cdn.playwright.dev`, and Microsoft's mirror `playwright.download.prss.microsoft.com` when the first one does not answer). Those servers see an ordinary web request.
4. Anthropic, only when you ask the source agent to work: you pressed Draft with agent, Fix this source with the agent or Draft one with the agent, and you added your own Anthropic API key in Settings › Agent. The app then sends to Anthropic's API (`api.anthropic.com`), under your key: the chapter page's HTML after trimming (styles, scripts without images and tracking removed), the site's series page when the app could read it (it reads it right after the chapter page and sends it trimmed the same way), a few counts the app took of the chapter page (numbers only, no page text), another page of the same site if the agent asks for it (at most three extra pages in a run), the chapter address, and the selectors the agent tries with the results of its own tests of them. When it repairs a saved source, it also sends that source's selectors and how the source fails. It does not send your library, your other sources, your phone, your logs or your settings. Your key goes to Anthropic and to no one else. Anthropic sees an ordinary web request, including your IP address, and handles what it receives under your agreement with Anthropic, not under this text; see the Console at `https://platform.claude.com`. The publisher receives none of it. The agent never runs during downloads, conversion, sync or prune, and nothing is sent to Anthropic when no key is saved.
5. Your phone, over the cable or on your local network. This does not go to the internet.

The Windows installer may also download Microsoft's WebView2 component from Microsoft at install time if your PC does not have it. That happens in the installer, not while the app runs.

Nothing else. The app contacts Anthropic only as item 4 describes: never at launch, never in the background and never without a saved key. The app sends no telemetry, usage statistics, crash reports or identifiers, and has no advertising.

## Diagnostics

Settings › About › Copy diagnostics copies a short text to your clipboard. It holds the app version, the runtime version, the tools version, the browser revision and the folders the app uses. It leaves out website addresses, source selectors, and all of a phone's ID except its last 4 characters. The app copies it only when you press the button, and it sends it nowhere: you paste it into a message yourself. Read it first. Folder paths can contain your user name.

## Removing your data

- Delete the library folder to remove your downloads and archives.
- Delete series folders on the iPhone in the reader app or in Finder or the Apple Devices app.
- Uninstall the app, then delete the app's data folder (Settings › About shows it before you uninstall) to remove your settings, sources, browser support and the source-agent spend file.
- If you added an Anthropic API key, choose Remove in Settings › Agent before you uninstall. The key is in your computer's credential store, not in the data folder, so deleting the folder does not remove it. If the app is already gone, delete the item named "Manga desk" in Keychain Access (Mac) or Credential Manager (Windows). You can also revoke the key in the Anthropic Console.

## Changes

If this text changes, the new text is published with the release that changes the behaviour.

## Contact

Contact the publisher through the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Do not post private information there.
