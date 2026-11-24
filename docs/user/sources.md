# Sources

A source tells Manga desk how one website lays out its chapter pages: where the page images are and where the link to the next chapter is. Without a source for a site, the app will not download from it.

## What the app does and does not do

- Manga desk ships no content, no catalog, no search and no list of websites. It has no built-in source for any site.
- You paste the addresses. You type a source or import one someone shared. Everything is stored on your computer.
- Only add a source for a site you have the right to copy from, and respect that site's terms.
- The app follows the site's robots.txt by default and paces its requests. See [robots.txt](#robotstxt) and [Pacing](#pacing-and-rate-limits).
- The app does not automate sign-in, get past a paywall or handle DRM. On macOS, the experimental browser-session option can retain cookies after you complete a site's browser verification yourself.
- The source agent is optional. It is off until you add your own Anthropic API key, it runs only when you press its button, and it can only propose a source for you to review. See [Draft a source with the agent](#draft-a-source-with-the-agent) and [What the agent sends and costs](#what-the-agent-sends-and-costs).

## Add a source

Open Sources in the top bar (Settings › Sources has Open Sources too). You can add, edit and duplicate sources there, use Import…, Export… and Delete…, and run Test. You can also add one during the first-launch steps. A source you have not saved stays open: the app asks before you leave Sources with changes that are not saved.

You can also let the optional agent draft a source from one chapter address. See [Draft a source with the agent](#draft-a-source-with-the-agent).

### The fields

| Field | What it is |
| --- | --- |
| Name | A label for you. Required. |
| Hosts | The site's host names without `https://` or any path, for example `example.org`. A source applies to an address when the address's host is one of these or ends with a dot and one of these, so `example.org` also covers `www.example.org`. If two sources match, the longest host wins. Required. |
| Image hosts | Other hosts the site's images come from, for example `img.example.org`. Leave empty if the images come from the site itself. |
| Page container | A selector for the part of the chapter page that holds the images. Required. |
| Page image | A selector for the images inside the container, such as `img`. Required. |
| Image attribute | Which attribute of the image holds its address. The default is `data-src`; if it is missing the app uses `src`. |
| Next chapter link | A selector for the link to the next chapter. Without it a download follows the Series chapters list when there is one, else one chapter per address. |
| Series title, Series cover, Series genres, Series chapters | Optional selectors for the series page. They fill in the title, the cover and the type, and let the app find chapters the next-links skipped. |
| Render mode | Auto, HTML or Browser. See below. |
| Script images | On by default. Before using a browser, the app reads the page list from a script on the page. Turn it off when a script on the site lists the wrong images. |
| Page-list attribute | The page container's attribute that names the site's page-list address, read before a browser. The default is `data-chapter-api`; leave it empty to skip that address. |
| Delays | The pause between chapters and between pages. See [Pacing](#pacing-and-rate-limits). |
| Respect robots.txt | On by default. See [robots.txt](#robotstxt). |

A selector is a short pattern that picks parts of a web page, such as `#pages` (the element with the id `pages`), `img` (all images) or `a.next` (links with the class `next`). To find the right ones, open a chapter page in your browser, right-click an image and choose Inspect (Inspect Element in Safari), and look at the elements around it. A site that changes its layout will need its source updated.

### Image hosts

For safety, the app contacts only the source's own site, its subdomains and the image hosts you list. It never contacts local or private network addresses. If a site serves its images from another host, add that host to Image hosts. Without it you will see a message that starts "Refused" and names the host (see [Troubleshooting](./troubleshooting.md)).

### Render mode

- Auto (the default): the app reads the page's HTML. If the image list is not there, it looks for a list in a script on the page or in a page-list address the site offers, and only then uses a browser. A browser needs [browser support](./browser-support.md).
- HTML: the app reads HTML and supported script or page-list data without running the site's JavaScript. An enabled verified session supplies the requests.
- Browser: the app always loads the page in a browser.

Some sites keep the chapter's page list in a script on the page; HTML mode with Script images on reads it
without running the site's JavaScript. Enable **Use saved browser session (experimental)** if the site asks
for browser verification. **Draft with agent** can fill these settings from a chapter URL; review its test
results and save the proposal. Haiku 5.5 is tried first in Auto mode, with Sonnet 5.5 available for harder
pages.

A 4xx response from `robots.txt` means that file is unavailable and supplies no rules, following
[RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html#section-2.3.1.3). Explicit disallow rules,
rate limiting (429), verification challenges, server errors and network failures still stop access.

## Test a source

Test checks a source on one chapter address without downloading anything.

1. Open the source and choose Test.
2. Paste the address of one chapter page.
3. Read the result.

Test loads the chapter page, and the series page if you set series fields. It downloads no images and writes no files. It follows the same robots.txt and pacing rules as a download. The result shows:

- How many pages it found, and the address of the first image.
- The next chapter link, if there is one. If the page has none but the series page lists the next chapter, Test shows that address and says where it came from.
- The series title and the number of chapters listed, if you set series fields. If you set Series cover or Series genres, Test also shows the cover's host and the genres it found.
- How the app read the page: HTML, a script on the page, a page-list address, or a browser. If the page needs a browser and none is set up, it says so.
- The robots.txt verdict: allowed, disallowed, ignored (you turned robots.txt off for this source), or unreachable (robots.txt could not be read).
- Warnings, such as a page count that does not match the page's own total.

A Test and a download never run at the same time, because the app makes one request at a time to a site. Test is unavailable while a download runs, and a download waits while a Test runs.

## Draft a source with the agent

The source agent reads one chapter page and the site's series page, proposes a source for the site, and tests the proposal on your chapter and, when it can find one, on one more. It is optional: you can always type or import a source, and the app works the same without it. The agent uses a Claude model from Anthropic, under an API key you add yourself. Everything it proposes is a draft: nothing is saved until you review it and press Save.

The agent runs only when you press Draft with agent, Fix this source with the agent or Draft one with the agent. It never runs during downloads, conversion, sync or prune.

### Set it up

1. Create an API key in your Anthropic account, in the Console at `https://platform.claude.com`. Set a spend limit there too (see [What the agent sends and costs](#what-the-agent-sends-and-costs)).
2. Open Settings › Agent. It says No key. Paste the key and choose Save key. It then says Key saved, and the app does not show the key again.
3. Choose a model: Auto (Haiku first, Sonnet if needed), Haiku or Sonnet.

The key goes into your Mac's credential store, the Keychain. The app does not write it to its settings or to any other file. To delete it, choose Remove, and then Remove key when the app asks "Remove the API key?". Drafting stops until you add a key again.

### Start a draft

1. Open Sources and choose Add source, or open a saved source.
2. Paste the address of one chapter page in the Test field.
3. Choose Draft with agent.

On a new source the agent drafts a whole source. On a saved source it repairs that source (see [Fix a source that stopped working](#fix-a-source-that-stopped-working)).

Progress lines appear under the Test row ("Reading the page", "Trying a profile (Haiku)", "Testing: …"), with a Stop button. Stop ends the draft, and nothing is saved. A draft is a job, like a download: Jobs lists it as Draft a source, with its log, its verdict, the agent's notes, its confidence, the number of calls and the cost; until you save or discard the proposal, Review in Sources takes you to it. Only one job runs at a time, so Draft with agent is unavailable while another job runs, and Test is unavailable while a draft runs. While a proposal is under review, Draft with agent waits until you save or discard it.

You can start a draft from two other places:

- Add series. If you press Start with an address whose site has no source, the dialog stays open and says "No source for <host>." with Draft one with the agent. It opens Sources with a new source, puts your address in the Test field and starts the draft. After you save the source, you are back in Add series with the address filled in.
- Jobs, to repair a source. See [Fix a source that stopped working](#fix-a-source-that-stopped-working).

With no key saved, all three buttons are disabled. A note says "No API key saved." and Open Settings › Agent takes you there.

### What a draft reads and tests

1. **The chapter page and the series page.** The agent reads the chapter page you pasted. After a short pause it reads the series page of the same site, worked out from the chapter address. If the app cannot work out a series address, or the series page cannot be read, the draft goes on without it.
2. **A proposal.** The model proposes selectors for both pages, so the source can also give the series title, cover, genres and chapter list.
3. **Your chapter.** The app tests the proposal on the chapter you pasted: it finds the page images, loads the first image and looks at the next chapter link, and reads the series fields you have set.
4. **One more chapter.** The app then tests the same proposal on a second chapter, to catch a source that fits only the chapter you pasted. It takes the chapter the next chapter link leads to, or else the next chapter in the series list, or else the previous one (so you can paste the newest chapter). If it finds none of these, only your chapter is tested, and the second chapter's row says why. Before it loads that chapter it waits, as a download waits between chapters: at least 5 seconds, even for a saved source that has Faster downloads on.
5. **Images.** The app checks the first image of each chapter and the series cover.
6. **Hosts.** The app, not the model, fills in Hosts and Image hosts from the addresses it saw. Hosts holds the host of your address, the host it redirected to, and the hosts on the same site of the next chapter, the series page and the second chapter, each only if a listed host does not cover it already. Image hosts holds the hosts outside the site that serve the page images of both chapters and the series cover. It never adds a local or private address. Every page image of both chapters must pass the same host rule a download uses; if one does not, the proposal fails and names the host.

For each proposal it tests, the agent makes a handful of page reads and a few small image checks (the first image of each chapter, rechecked when a test is repeated, and the cover), all under the pacing of a download. An image check reads only the start of the image, so no image is downloaded.

### What the agent can and cannot do

- It proposes selectors for the chapter page and the series page (Series title, Series cover, Series genres, Series chapters), the render mode and the two page-list settings (Script images, Page-list attribute). The app fills in Hosts and Image hosts from the addresses its own tests saw, as described above.
- It reads only pages of that site and its subdomains, through the same request code as a download. It always follows robots.txt, even for a saved source that has the override, never shortens a Crawl-delay and keeps the pacing limits. See [robots.txt](#robotstxt) and [Pacing](#pacing-and-rate-limits).
- It cannot turn robots.txt off, lower the delays or handle logins. A new source keeps the default delays and Respect robots.txt on. A repair keeps the saved source's own settings.
- What it returns is a proposal. The app tests it itself before showing it, and nothing is saved until you press Save.
- You are responsible for the sites you add and download from, whether you typed the source or the agent drafted it. See [What the app does and does not do](#what-the-app-does-and-does-not-do) and the [Terms](../legal/terms.md).

### If the page needs a browser

Some sites build their page list with JavaScript. If the agent finds that and browser support is not installed, the review says "The page needs browser support." and the proposal sets Render mode to Browser. It does not pass the test. Choose Open Settings › Browser support, install it (see [Browser support](./browser-support.md)), then draft again. With browser support installed, the agent's test can use the browser.

## Review before saving

When a draft ends, the proposed values are in the editor's fields, where you can still change them, and an Agent proposal appears under the Test row. It shows:

- A verdict: "The proposal passed the test." or "The proposal did not pass the test." A draft with no usable proposal leads with a headline that says what happened instead; see [When a draft gives no proposal](#when-a-draft-gives-no-proposal). "Stopped." means you pressed Stop. With no proposal there is nothing to save: the fields are as they were, and Dismiss clears the notice.
- What was tested: a count of each status, for example "12 tested" and "1 check this", then every check as a row under three heads: Chapter page, Series page and Hosts. See [What was tested](#what-was-tested).
- The final test, laid out as Test shows it: pages found, the first image, the next chapter link, how the page was read, the robots.txt verdict and any warnings.
- The agent's notes, as plain text.
- Its confidence (high, medium or low), which is the agent's own estimate, and the cost of the draft.

### What was tested

Each row is a status word and one sentence from the app, written with the editor's own labels. The rows come in three groups:

- **Chapter page**: the page images and where the list came from, Image attribute, how the page was read, the order of the pages, the first image, Next chapter link and the second chapter.
- **Series page**: whether the series page was read, then Series title, Series chapters (how many chapters, and whether yours is among them), Series cover (and whether it loads) and Series genres (with the series type they give).
- **Hosts**: the Hosts and why each is there, and the Image hosts and where each was seen (page images, series cover).

The status words:

| Word | What it means | Example |
| --- | --- | --- |
| tested | The check ran and found what the source needs. | "Next chapter link leads to `https://example.org/series/chapter-2`." |
| check this | The check ran and found something worth a look. It does not stop the proposal from passing. | "Series title matches no text on the series page." |
| not found | The proposal leaves an optional field empty, or the check found nothing for it. The sentence says what the app does without it. | "Series cover is not set; the series then has no cover image." |
| failed | The proposal does not pass. | "The second chapter `https://example.org/series/chapter-2` gives the same 32 page images as the first chapter, so the selectors do not follow the chapter." |
| not tested | The check did not run, and the sentence says why. | "The second chapter was not tested because a first-chapter check failed." |

While the proposal is in the fields, a field that a check marked check this, not found or failed shows that word under its label. The fields stay editable: change any of them before you Save, and run Test on your chapter to try the change. The marks go away when you Save or Discard.

A proposal passes only when none of its checks failed, and the app's own tests decide, not the agent's claim. A check fails when the chapter page has no page images or the test stopped on an error; when the first image does not load, is not an image or is only a placeholder; when Next chapter link leads off the site, back to the same chapter, or to the series page unless the series list shows your chapter as the newest; when the second chapter has no page images, gives the same images as your chapter or has a first image that does not load; or when a page image is on a host a download would refuse. A series with a single chapter (no Next chapter link and at most one chapter listed) can pass with the second chapter marked not tested. With no usable Next chapter link and a series list that does not show your chapter, a proposal can pass with only your chapter tested; the second chapter is marked check this and says so. A second chapter that robots.txt does not allow is marked check this, not failed: no change to the source could fix that, and the sentence says a download will be refused there too. Every other row marked check this, not found or not tested is yours to look at; it does not stop a proposal from passing.

Choose Save source (Save changes for a repair) to keep it, or Discard to put the earlier fields back. Save runs the same checks as a source you typed. Discard saves nothing and sends nothing. When the test did not pass, Discard is the highlighted choice, but you can still edit the fields and save.

Read the proposal as you would an imported source. Check that Hosts names the site you meant and that you recognise each Image host. The agent has tested your chapter and, unless the second chapter's row says otherwise, one more; after you save, you can run Test on another chapter from further along the series.

### When a draft gives no proposal

When the app can tell why a draft ended without a usable proposal, the review leads with a headline, then what it means, then the app's own sentence about this draft, then the one thing to do. [Troubleshooting](./troubleshooting.md#the-agent-could-not-draft-a-source) has the same entries.

- **The site asks for browser verification.** The site answered with a verification check instead of the page, and the app never answers one. Choose Verify in browser, complete the check in the window that opens and finish in Jobs. Then come back to this source, tick Use saved browser session and draft again. If the review says the saved session has no verification yet, or that it has run out, verify again and keep the box ticked. This is experimental and works on macOS only; see [Saved browser sessions](./browser-support.md#saved-browser-sessions-experimental).
- **The page needs browser support.** The page builds its images with JavaScript and browser support is not installed. Choose Open Settings › Browser support, set it up, then draft again. See [If the page needs a browser](#if-the-page-needs-a-browser).
- **The app cannot download from this page.** The review says that the page draws its images in the browser instead of linking image files, that its image addresses answer with something that is not an image, or that its images show only in a browser, which the app cannot use together with a saved browser session. Nothing in the fields can fix this, and neither Verify in browser nor browser support makes it work. Stop here: another draft of the same page will say the same.
- **robots.txt does not allow this page.** The site asks automated tools not to fetch the page, so the app did not fetch it. The draft cost nothing if robots.txt refused the page you pasted at the start, before the agent was asked anything; if it refused a later test, the draft stopped there and the review shows the cost so far. A draft always follows robots.txt, with no override. Check that you pasted the address you meant. If the headline is "robots.txt could not be read.", draft again later.
- **The site refused the page.** The page asks for a sign-in, or the site answered that the page is forbidden. The app does not sign in to sites. Use a chapter page that opens without signing in.
- **The chapter page did not load.** The site answered with an error, such as page not found, or it could not be reached, and the draft cost nothing. Check the address and your connection, then draft again.
- **No proposal passed the test.** The agent made its attempts and none passed. The review says which part the last proposal failed on, for example "The last proposal failed on the second chapter.", and the row marked failed has the sentence. Try the address of a different chapter, choose Sonnet in Settings › Agent, or edit the fields yourself and use Test.

A few other headlines have their own entries in [Troubleshooting](./troubleshooting.md#the-agent-could-not-draft-a-source): "The agent is not set up.", "The draft reached its limit.", "The model was not available.", "The saved browser session could not be opened." and "The draft failed."

## Fix a source that stopped working

A site that changes its layout breaks its source, and a download then fails with "No page images found; check PAGE_CONTAINER and PAGE_IMAGE." If a saved source covers the series' site, Jobs shows the failed job with Fix this source with the agent. The button is disabled, with a note, until you have added a key.

Choosing it opens that source in Sources, puts a chapter address of the series in the Test field (for Add series, the address you pasted) and starts the draft. If the app has no chapter address for the series, it leaves the field empty and asks you to "Paste a chapter URL to fix from." With a saved source open in Sources, Draft with agent does the same repair.

A repair starts by testing the saved source ("Testing the saved source: …"), then asks the agent for the smallest change that makes the test pass. The review lists only the fields that change, each as old → new, and shows "empty" for a field the repair clears. If nothing needs to change it says "The agent proposes no change." Everything else stays as saved, including the delays and the robots.txt setting. A repair is tested on a second chapter too, and the review lists the same checks as for a new source. Choose Save changes or Discard.

## What the agent sends and costs

### What is sent

When you run the agent, it sends this to Anthropic, under your own API key:

- the chapter page's HTML after trimming (styles, scripts that hold no images, and tracking removed; a very long page is cut down to its outline and the parts around its images);
- the site's series page, trimmed the same way, when the app could read it. The app reads it right after the chapter page and sends it with the chapter page;
- a few counts the app took of the chapter page, such as how many images it holds (numbers only, no page text);
- another page of the same site, such as a second chapter page, if the agent asks for it (at most three extra pages in a run);
- the chapter address;
- the selectors it tries, with the results of its own tests of them, such as how many pages were found and the sentences of the review's checks. When it repairs a saved source, it also sends that source's selectors and how the source fails.

It does not send your library, your other sources, your phone, your logs or your settings. Your key goes to Anthropic and to no one else. Nothing is sent when the agent is not running. Anthropic handles what it receives under your agreement with Anthropic; see the Console at `https://platform.claude.com`. [Privacy](../legal/privacy.md) lists everything the app sends.

A web page can try to give the agent orders. That is why the agent can only read pages of the same site and hand back a source: the app tests the source, and you review it before it is saved.

### What it costs

Anthropic charges your account for each model call. Manga desk adds nothing.

- A draft costs about 2–3 cents with Haiku and about 40–50 cents with Sonnet (US dollars). Auto starts with Haiku and moves to Sonnet only if Haiku's attempts fail, so a hard site costs more.
- The series page makes the first message longer, so each model call carries more text. The cap on one draft has not changed: a run stops at 8 model calls or about US$0.75, whichever comes first. The calls already made are charged. The app's own page reads and image checks are not charged by Anthropic.
- Settings › Agent shows "Spent this month", and each review shows the cost of its draft. Both are estimates from the token counts the API reports, at the prices built into the app (checked on 8 November 2026). Your Anthropic bill is the figure that counts, and prices can change after this version.
- The app keeps the monthly figure in a file in its data folder, `agent-usage.jsonl`: token counts and cost only, no page content.

Set a spend limit in the Anthropic Console as well. The cap of about US$0.75 protects one draft, not your month.

## Share a source

Use Export… to save a source as a file. Use Import… to add a source from a file someone gave you. Read an imported source before you use it: check its hosts and whether robots.txt is on. You are responsible for what you run with it.

## robots.txt

Most sites publish a file called robots.txt that says which parts of the site automated tools may fetch. Manga desk checks it before it makes a request, for chapter pages, images, redirects and every request a browser makes. If robots.txt does not allow a page, the run stops with a message like "robots.txt disallows <address>; stopping." Nothing is fetched from that page. A site with no robots.txt allows everything. If robots.txt cannot be read because of a server error, the run stops.

### Crawl-delay

If robots.txt asks for a pause between requests (`Crawl-delay`), the app waits at least that long between its requests to the site. It never shortens the pause. If a site asks for more than 60 seconds between requests, the run stops with a message that names the delay.

### The robots.txt override

A source can have Respect robots.txt turned off. This is the robots.txt override. The app asks you to acknowledge it first and stores the date. The override is shown on the source, and every run that uses it says so in its log.

A source imported from an earlier Manga desk setup that ignored robots.txt arrives with Respect robots.txt off but without your acknowledgement, so it cannot be saved yet. Choose Confirm override… to acknowledge it, or turn Respect robots.txt on.

What the override means:

- The site's owner has asked automated tools not to fetch some paths. With the override, the app fetches them anyway.
- It is your decision and your responsibility. Do not use it unless you have the right to copy the material and permission to fetch it this way.
- It does not get past logins, errors or access controls.

## Pacing and rate limits

- By default, the app downloads one image at a time.
- By default, it waits at least 5 seconds between chapters and at least 0.5 seconds between pages. The usual pauses are 5 to 10 seconds between chapters and 0.5 to 1.5 seconds between pages. A delay you set below these limits is raised to the limit, with a warning.
- With **Use saved browser session** enabled, **Faster downloads (2 images at once)** sets pauses to 0.15–0.35 seconds between pages and 1–2 seconds between chapters. It allows up to two image downloads, with at most four request starts per second per host. You can increase those pauses in the delay fields.
- If the faster mode encounters a request or image error, it drops to one image at a time for the rest of the run. Requests to the affected host wait at least one second apart, doubling after further errors up to 30 seconds. Queued requests share the cooldown. A new run starts at the selected speed again. Browser verification challenges still stop the job. A page image that arrives whole but is only a few bytes (a placeholder the site serves in place of a page) fails that page without slowing the run.
- If a site answers with HTTP 429 or 503 (too many requests, or busy), the whole run pauses for the time the site asks, or 60 seconds, whichever is longer. Each further pause doubles, up to 15 minutes.
- The run stops by itself, cleanly, after five pauses, if a site asks for a wait over 15 minutes, or if five images in a row fail. Run it again later. Finished chapters are not downloaded again.

## No source for a site

If you paste an address whose host matches no source, the run stops before it makes any request, with "No source profile for <host>". Add or import a source for that site under Sources.

In Add series the app checks the address when you press Start. The dialog stays open, nothing starts, and it says "No source for <host>." Add or import a source, or, if you have set up the agent, choose Draft one with the agent. See [Draft a source with the agent](#draft-a-source-with-the-agent).
