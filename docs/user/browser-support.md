# Browser support

Most sources work without a browser: the app reads the page's HTML directly. A few sites build their page list with JavaScript and need a real browser to show it. Browser support is optional and is not part of the installer.

## Do you need it?

You need it when:

- Test on a source says the page needs a browser and none is set up.
- A download stops with a message that starts "Browser support is not installed".

If your source's render mode is HTML, it never needs a browser. See [Sources](./sources.md).

## Set it up

Open Settings › Browser support. You have three choices.

### Install browser support

Choose Install browser support. The app downloads a small headless browser (a browser with no window) and keeps it in its own folder.

- The download is roughly 80 MB, and it takes roughly 200 MB on disk. The button shows the size for your computer.
- It downloads from Playwright's download servers (`cdn.playwright.dev`, or Microsoft's mirror `playwright.download.prss.microsoft.com` if the first one does not answer). You need an internet connection.
- You see progress and can stop the download.
- Settings › About shows the installed browser revision.
- If you switched to Chrome or Edge and the app's own browser is still there, choose Use installed browser support to go back to it.

### Use installed Chrome or Microsoft Edge

If you already have Google Chrome, choose Use installed Chrome. On Windows, Microsoft Edge is already installed, so choose Use Microsoft Edge. Nothing is downloaded.

If the app says it cannot launch the browser, check that the browser is installed and up to date, or install browser support instead.

### Not now

In the first-launch steps, choose Not now and set it up later, when a source needs it. Not now is hidden while the install runs.

## What the browser is used for

The browser only loads pages from your sources. It is not used to download images: the app does that itself, and images, media and fonts are blocked in the browser. The browser follows the same robots.txt rules as the rest of the app, at every redirect. A page that needs a redirected script or frame to work may not work in browser mode. Try the HTML render mode, or another source.

## Remove it

Open Settings › Browser support and choose Remove. This deletes the browser the app installed and frees the disk space. Remove is not available while a job is running. Sources that need a browser will fail until you install or choose one again.
