# Troubleshooting

Find the message or symptom you see. Each section says what it means and what to do.

Install problems:

- [macOS says it cannot check the app, or that it is damaged](#macos-gatekeeper)

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

Source agent problems:

- [The agent could not draft a source](#the-agent-could-not-draft-a-source)
- [The agent says the site asks for browser verification](#the-agent-says-the-site-asks-for-browser-verification)
- [The agent says the page needs browser support](#the-agent-says-the-page-needs-browser-support)
- [The agent says it cannot download from the page](#the-agent-says-it-cannot-download-from-the-page)
- [The agent says robots.txt does not allow the page](#the-agent-says-robotstxt-does-not-allow-the-page)
- [The agent says the site refused the page](#the-agent-says-the-site-refused-the-page)
- [The agent says the chapter page did not load](#the-agent-says-the-chapter-page-did-not-load)
- [The API key is refused or missing](#the-api-key-is-refused-or-missing)

Finding information:

- [Where the logs are](#where-the-logs-are)
- [Copy diagnostics](#copy-diagnostics)

## macOS Gatekeeper

macOS shows one of two messages that mean different things. "Apple cannot check it for malicious software" should not appear for a release from the releases page. "Manga desk is damaged and can't be opened" is never to be overridden. Both are explained step by step in [Install on macOS](./install-macos.md).

## The app cannot find the iPhone

The message reads like "No iPhone <name> is connected". Check these in order:

1. The cable is plugged into the computer and the iPhone, and the cable carries data (some cables only charge).
2. The iPhone is unlocked.
3. On the iPhone you tapped Trust (see the next sections).
4. Finder shows the iPhone in its sidebar.
5. Refresh the list in Settings › iPhone.

If you use Wi-Fi sync, the phone must be on the same network with Wi-Fi sync turned on in Finder. Wi-Fi is best effort, and the cable is more reliable.

## The iPhone has not trusted this computer

The message says the iPhone has not trusted this computer yet.

1. Unlock the iPhone and connect it with the cable.
2. Open Finder.
3. Tap Trust on the iPhone and enter its passcode.
4. Try again.

If the question does not appear, unplug the cable, plug it in again, and unlock the phone.

## The iPhone is locked

The message reads "The iPhone <name> is locked. Unlock it, keep it unlocked while it syncs, and try again." Unlock the iPhone, keep it unlocked until the sync ends, and start the sync again. Finished files are not copied again.

## The Apple device service is missing

The message reads "Cannot reach the Apple device service (usbmuxd)." followed by a hint.

The service is part of macOS. Connect the iPhone with a cable, open Finder once so that it shows the iPhone, then try again.

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

The message starts "Browser support is not installed". The page needs a browser and none is set up. Open Settings › Browser support and install it or choose Chrome. See [Browser support](./browser-support.md). If a source works as HTML, set its render mode to HTML.

## No source profile for a host

The message reads "No source profile for <host>". The address you pasted has a host that no source covers, so the app stopped before it made any request.

1. Open Sources in the top bar.
2. Add or import a source whose Hosts include that host or its parent. For `www.example.org`, a source for `example.org` is enough. Or, if you have set up the source agent, draft one: see [Draft a source with the agent](./sources.md#draft-a-source-with-the-agent).
3. Try again.

When several series are downloaded together, the series with the missing source fails and the others still run.

## A host is refused

The message reads "Refused <host>: not the start site; add it to ALLOWED_HOSTS if it is the site's image host". The page points at a host that is not the source's site, its subdomains or one of its image hosts. If it is the site's image host, add it to Image hosts in the source. The log message calls this setting ALLOWED_HOSTS. Do not add a host you do not know.

A message like "Refused <host>: resolves to <address>" means the address is on a private or local network. The app never contacts those, on purpose.

## No page images found

The message reads "No page images found; check PAGE_CONTAINER and PAGE_IMAGE." The page container or page image selector found nothing. Use Test on the chapter address and change the selectors. If the page lists its images with JavaScript, set the render mode to Auto or Browser and set up [browser support](./browser-support.md).

If the site changed its layout and a saved source covers it, Jobs shows Fix this source with the agent under the failed job (disabled until you have added an API key). See [Fix a source that stopped working](./sources.md#fix-a-source-that-stopped-working).

## Images fail in a row

The message reads "<number> images failed in a row; rerun later to resume." The site stopped serving images, the address changed, or the network dropped. Rerun later. A run keeps what it has and picks up from there.

## The agent could not draft a source

The review says "No proposal passed the test." or "The proposal did not pass the test.", or it says "The draft reached its limit.", "The model was not available." or "The draft failed.", or the progress ends with "Failed". The review lists the app's checks under the verdict, and the row marked failed says which part went wrong. The whole run is in Jobs under Draft a source. The calls the agent made are charged to your Anthropic account even when nothing passed.

- "The last proposal failed on …" or "The agent found no profile to test on this page." The agent made its attempts and none passed. Look at the row marked failed (below), try the address of a different chapter, or edit the fields yourself and use Test.
- "No page images found; check Page container and Page image." The agent's own test found no images with the selectors it tried.
- A row about the first image. The selectors found an image address, but the first image was not an image, was only a few bytes (a placeholder) or could not be loaded. The site may refuse it, or it may come from a host that needs to be listed in Image hosts.
- A row about Next chapter link. The link leads off the site, back to the same chapter, or to the series page although a later chapter exists. Edit Next chapter link so that it picks the link to the next chapter.
- A row about the second chapter. The selectors worked on the chapter you pasted, but the second chapter has no page images, gives the same page images as the first chapter, or its first image did not load. The selectors may fit one chapter only. Draft from a different chapter, or edit the selectors and use Test. A second chapter that robots.txt does not allow is shown as check this, not failed: the app did not test it, and a download will be refused there too.
- A row about Image hosts. A page image is on a host a download would refuse, such as a local or private address, or on a host that kept changing between the app's tests. The app does not add such a host. Do not add a host you do not know.
- "The draft reached its limit." The run used all of its 8 model calls, or it stopped before a call that could have taken it past about US$0.75. If it has a best proposal, the review shows it. For a hard site, choose Sonnet in Settings › Agent and draft again (about 40–50 cents), or edit the source yourself.
- "Stopped." You pressed Stop. Nothing is saved.
- "The model was not available." Anthropic did not accept the request or could not be reached. Read Anthropic's message under the headline. If it is about credit or a spend limit, fix that in the Console at `https://platform.claude.com`; otherwise wait a few minutes and draft again. The Jobs log may say "Rate limited by Anthropic". A proposal the agent made before this stays in the review.
- "The saved browser session could not be opened." The sentence under it says why, for example that no Chrome or Edge is available, that the session's browser is still open, or that saved sessions are not available on this computer. Fix what it names and draft again. See [Saved browser sessions](./browser-support.md#saved-browser-sessions-experimental).
- "The draft failed." The draft ended on an error, which the review shows under the headline. Read it, then draft again or edit the source yourself.
- A message from Anthropic, for example about a spend limit or credit. It is shown as Anthropic wrote it. Check your account in the Console at `https://platform.claude.com`.

When the app cannot read the chapter page at the start, the headline says why, and the agent made no model call, so it cost nothing. See the entries for [robots.txt](#the-agent-says-robotstxt-does-not-allow-the-page), [a page that refuses the app](#the-agent-says-the-site-refused-the-page) and [a chapter page that did not load](#the-agent-says-the-chapter-page-did-not-load).

You can still save a proposal that did not pass and edit it, but check it with Test first. See [Review before saving](./sources.md#review-before-saving).

## The agent says the site asks for browser verification

The review says "The site asks for browser verification." The site answered with a verification check instead of the page, or the source's saved browser session has no verification yet or has run out. The app never answers a verification check.

1. Choose Verify in browser, in the review or next to the Test field. A browser window opens on the Test address.
2. Complete the site's verification yourself. When the page opens, go to Jobs and choose Verification finished — continue.
3. Come back to this source, tick Use saved browser session and draft again. If the review says the saved session has no verification yet or that it has run out, verify again and keep the box ticked.

Saved browser sessions are experimental and work on macOS only, and a site can ask again later. See [Saved browser sessions](./browser-support.md#saved-browser-sessions-experimental).

## The agent says the page needs browser support

The review says "The page needs browser support." and the Chapter page group says the page builds its images with JavaScript and browser support is not installed. The proposal sets Render mode to Browser, and it does not pass because the app cannot test it without a browser.

1. Choose Open Settings › Browser support, then install browser support or choose Chrome. See [Browser support](./browser-support.md).
2. Draft again from the same chapter address.

## The agent says it cannot download from the page

The review says "The app cannot download from this page." and gives one of these reasons: the page draws its images in the browser instead of linking image files, so there is no image address to save; the page's image addresses answer with something that is not an image; or the page shows its images only in a browser, which the app cannot use together with a saved browser session.

There is nothing to change in the fields, and another draft of the same page will say the same. Neither Verify in browser nor browser support makes such a page work, so do not set either up for this. Use a different page or site, or do not download from this one.

## The agent says robots.txt does not allow the page

The review says "robots.txt does not allow this page." The site's robots.txt asks automated tools not to fetch the chapter page, so the app did not fetch it. If robots.txt refused the page you pasted when the app first read it, before the agent was asked anything, the draft cost nothing. If it refused a later test, the draft stopped there, and the review shows what the draft cost so far. A draft always follows robots.txt, even for a saved source that has the override, so there is nothing to turn off here. Check that you pasted the address you meant. See also [robots.txt disallows a page](#robotstxt-disallows-a-page).

If the headline says "robots.txt could not be read.", the site's robots.txt did not answer properly. The app does not fetch a page without it. Draft again later.

## The agent says the site refused the page

The review says "The site refused the page." and under it that the page asks for a sign-in (the site answered HTTP 401), or that the site answered that the page is forbidden (HTTP 403, without a verification page). The app does not sign in to sites. Use a chapter page that opens in your browser without signing in. The draft stopped at the chapter page, so it cost nothing.

## The agent says the chapter page did not load

The review says "The chapter page did not load." The site answered with an error, such as page not found, or it could not be reached, and the draft cost nothing. Check the address for typing mistakes and your connection, and check that the page opens in your browser. Then draft again, later if the site is down.

## The API key is refused or missing

When the key is missing or refused, the review says "The agent is not set up." and the sentence under it says which.

- "The API key was refused by Anthropic." Anthropic did not accept the key: it may have been mistyped, deleted or revoked, or belong to an account that cannot use the API. Create a key in the Console at `https://platform.claude.com`. In Settings › Agent choose Remove, then paste the new key and choose Save key. The app does not show a saved key, so to replace one you remove it first.
- "No API key. Add one in Settings › Agent." No key is saved, or it was removed while the draft waited. With no key, Draft with agent, Fix this source with the agent and Draft one with the agent are disabled and say "Add an API key in Settings › Agent to draft sources with the agent."
- A message such as "Cannot read the API key from the credential store", "Cannot save the API key in the credential store" or "The credential store is not available". The Keychain did not do what the app asked. Make sure the Keychain is unlocked, then try again.

The key is never written to a file or a log. See [Privacy](../legal/privacy.md).

## Where the logs are

- The Jobs screen shows the output of each job while the app is open. Job output is not saved to a file. The app's own messages (its start-up line, updates and errors) go to `logs/manga-desk.log` in its app data folder, which Settings › About shows; that file starts again at each launch.
- The downloader also writes a log file for every series, `downloads/<series>/scrape.log`, and a one-line summary per run in `downloads/scrape.log`. Both are inside your library folder. Settings › Library folder shows where it is.

Log files can contain website addresses. Read them before you share them.

## Copy diagnostics

Open Settings › About and choose Copy diagnostics. The app copies a short text to your clipboard. It lists the app version, the runtime version, the tools version, the browser revision and the folders the app uses. It leaves out website addresses, source selectors and all but the last 4 characters of a phone's ID. Nothing is sent anywhere: you paste it into your problem report yourself.

Read the text before you paste it. Folder paths can contain your user name.
