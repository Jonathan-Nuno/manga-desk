# FAQ

## Does Manga desk include manga or a list of sites?

No. It ships no content, no catalog, no search and no list of websites. You paste addresses and set up the sources yourself.

## Is it free?

Yes. Manga desk is free to use and its source code is not public. The [Terms](../legal/terms.md) say what you may do with it.

## Do I need an API key, and what does it cost?

Only for the optional source agent, which drafts a source from a chapter address. Without a key you can use everything else: you type or import sources yourself, and Settings › Agent just says No key. With the agent you add your own Anthropic API key in Settings › Agent, and Anthropic bills your account for each draft: about 2–3 cents with Haiku, about 40–50 cents with Sonnet. A draft stops at 8 model calls or about US$0.75. Set a spend limit in the Anthropic Console too. See [What the agent sends and costs](./sources.md#what-the-agent-sends-and-costs).

## Which sites does it work with?

That depends on the sources you set up. The app does not provide or recommend any. See [Sources](./sources.md).

## Is it legal to download from a site?

That depends on the material, the site's terms and the laws where you live. Manga desk cannot tell you, and nothing in this guide is legal advice. Only download material you have the right to copy. You are responsible for what you add and download.

## Why is it slow?

On purpose. The app downloads one page at a time, waits between pages and chapters, follows the site's robots.txt and backs off when a site asks it to. See [Sources](./sources.md).

## Can it log in to a site, or download paid or protected chapters?

It does not automate sign-in, get past paywalls or handle DRM. For a browser verification screen, you can try the experimental [saved browser session](./browser-support.md#saved-browser-sessions-experimental). You complete verification yourself; the app keeps that separate browser profile locally and reuses its cookies for downloads. Sites can require verification again.

## Do I need an iPhone?

No. Without a phone, the `library` folder holds `.cbz` files that any comic reader that opens `.cbz` can use. See [Set up your iPhone](./iphone.md) for ways to copy them.

## Which reader apps work?

Readers on the iPhone that support file sharing. Inkshelf is the suggested one and is preselected when the app finds it. Get it from the App Store: [Inkshelf: Manga & Comic Reader](https://apps.apple.com/us/app/inkshelf-manga-comic-reader/id6824132149). Only apps with file sharing appear in the list in Settings › iPhone.

## Does it work with Wi-Fi?

The cable is the supported way. Wi-Fi sync can work when the phone is on the same network and Wi-Fi sync is on in Finder, but it is best effort.

## Does the sync delete anything on my phone?

No, apart from its own leftover temporary files from an interrupted copy. See [Set up your iPhone](./iphone.md).

## Where are my files?

In your library folder (Settings › Library folder shows it). `downloads` holds page images and `library` holds the `.cbz` archives. The app's own settings and source profiles are in a separate folder that Settings › About shows.

## How do I free up disk space?

Open Storage. Once a chapter has an archive in `library`, Prune can remove its original page images. Pruned chapters are still treated as done. You can also delete a series folder yourself.

## Does Manga desk collect data about me?

No. It has no telemetry, analytics or accounts. See [Privacy](../legal/privacy.md) for exactly what goes over the network.

## Is my library, or anything else, sent to Anthropic?

No. The agent runs only when you press Draft with agent, Fix this source with the agent or Draft one with the agent, never during downloads, conversion, sync or prune. Then it sends Anthropic the chapter page's HTML after trimming, the site's series page when the app could read it, any other page of the same site it asks for, a few counts the app took of the chapter page, the chapter address and the selectors it tries with the results of its own tests. It does not send your library, your other sources, your phone or your logs. Anthropic handles what it receives under your agreement with Anthropic. See [Privacy](../legal/privacy.md).

## Can I use it on Linux, Android or iPad?

No. Manga desk is a Mac app. The iPhone is only where your reader app runs.

## Is there a Windows version?

Manga desk is not available for Windows.

## How do I update it?

The app checks once a day and asks before it installs. See [Updates](./updates.md).

## How do I uninstall it?

See [Install on macOS](./install-macos.md). Your library folder is never deleted by the app.

## How do I report a problem?

Open an issue in the releases repository: `https://github.com/Jonathan-Nuno/manga-desk`. Add the text from Settings › About › Copy diagnostics, and say what you did and what you saw.
