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
- If you switched to Chrome and the app's own browser is still there, choose Use installed browser support to go back to it.

### Use installed Chrome

If you already have Google Chrome, choose Use installed Chrome. Nothing is downloaded.

If the app says it cannot launch the browser, check that the browser is installed and up to date, or install browser support instead.

### Not now

In the first-launch steps, choose Not now and set it up later, when a source needs it. Not now is hidden while the install runs.

## What the browser is used for

The browser only loads pages from your sources. It is not used to download images: the app does that itself, and images, media and fonts are blocked in the browser. The browser follows the same robots.txt rules as the rest of the app, at every redirect. A page that needs a redirected script or frame to work may not work in browser mode. Try the HTML render mode, or another source.

## Remove it

Open Settings › Browser support and choose Remove. This deletes the browser the app installed and frees the disk space. Remove is not available while a job is running. Sources that need a browser will fail until you install or choose one again.

## Saved browser sessions (experimental)

On macOS, a source that shows a browser verification screen can use a separate, persistent Chrome or Edge profile. Install Chrome first. This is separate from the hidden browser described above.

1. Save the source, then enter a chapter address in its Test field and choose **Verify in browser**.
2. Complete the site's verification in the separate browser window. Once the source page opens, return to Jobs and choose **Verification finished — continue**.
3. When the job says the session is saved, return to the source, enable **Use saved browser session (experimental)** and save it. Use HTML or Auto render mode.
4. Test or download normally. The browser opens briefly with its own profile for each run. Chapter pages, series pages, images and robots.txt requests reuse its cookie jar. If verification expires, the job stops; verify the source again.

Profiles live under `browser-sessions/` in the app's data folder (Settings › About). Each origin has a separate profile. The app does not read your usual Chrome/Edge profile. Session files are not included in source exports or diagnostics. To forget sessions, stop all jobs, quit the app and delete that folder. Removing the optional headless browser does not delete these profiles.

This prototype currently supports macOS and HTML/inline-script/API page lists, not full JavaScript chapter rendering. The request adapter buffers responses before checking their size; it is experimental and not yet a streaming replacement. Sites may reject session-backed requests or require verification again; a saved session is not a permanent exemption.
