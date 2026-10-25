# Sources

A source tells Manga desk how one website lays out its chapter pages: where the page images are and where the link to the next chapter is. Without a source for a site, the app will not download from it.

## What the app does and does not do

- Manga desk ships no content, no catalog, no search and no list of websites. It has no built-in source for any site.
- You paste the addresses. You type a source or import one someone shared. Everything is stored on your computer.
- Only add a source for a site you have the right to copy from, and respect that site's terms.
- The app follows the site's robots.txt by default and paces its requests. See [robots.txt](#robotstxt) and [Pacing](#pacing-and-rate-limits).
- The app does not log in, keep cookies, get past a paywall or handle DRM. Pages that need any of these will not work, and support for them will not be added.

## Add a source

Open Sources in the top bar (Settings › Sources has Open Sources too). You can add, edit and duplicate sources there, use Import…, Export… and Delete…, and run Test. You can also add one during the first-launch steps. A source you have not saved stays open: the app asks before you leave Sources with changes that are not saved.

### The fields

| Field | What it is |
| --- | --- |
| Name | A label for you. |
| Hosts | The site's host names without `https://` or any path, for example `example.org`. A source applies to an address when the address's host is one of these or ends with a dot and one of these, so `example.org` also covers `www.example.org`. If two sources match, the longest host wins. |
| Image hosts | Other hosts the site's images come from, for example `img.example.org`. Leave empty if the images come from the site itself. |
| Page container | A selector for the part of the chapter page that holds the images. Required. |
| Page image | A selector for the images inside the container, such as `img`. Required. |
| Image attribute | Which attribute of the image holds its address. The default is `data-src`; if it is missing the app uses `src`. |
| Next chapter link | A selector for the link to the next chapter. Without it the app downloads one chapter per address. |
| Series title, Series cover, Series genres, Series chapters | Optional selectors for the series page. They fill in the title, the cover and the type, and let the app find chapters the next-links skipped. |
| Render mode | Auto, HTML or Browser. See below. |
| Delays | The pause between chapters and between pages. See [Pacing](#pacing-and-rate-limits). |
| Respect robots.txt | On by default. See [robots.txt](#robotstxt). |

A selector is a short pattern that picks parts of a web page, such as `#pages` (the element with the id `pages`), `img` (all images) or `a.next` (links with the class `next`). To find the right ones, open a chapter page in your browser, right-click an image and choose Inspect, and look at the elements around it. A site that changes its layout will need its source updated.

### Image hosts

For safety, the app contacts only the source's own site, its subdomains and the image hosts you list. It never contacts local or private network addresses. If a site serves its images from another host, add that host to Image hosts. Without it you will see a message that starts "Refused" and names the host (see [Troubleshooting](./troubleshooting.md)).

### Render mode

- Auto (the default): the app reads the page's HTML. If the image list is not there, it looks for a list in a script on the page or in a page-list address the site offers, and only then uses a browser. A browser needs [browser support](./browser-support.md).
- HTML: the app only reads the page's HTML and never uses a browser.
- Browser: the app always loads the page in a browser.

## Test a source

Test checks a source on one chapter address without downloading anything.

1. Open the source and choose Test.
2. Paste the address of one chapter page.
3. Read the result.

Test loads the chapter page, and the series page if you set series fields. It downloads no images and writes no files. It follows the same robots.txt and pacing rules as a download. The result shows:

- How many pages it found, and the address of the first image.
- The next chapter link, if there is one.
- The series title and the number of chapters listed, if you set series fields.
- How the app read the page: HTML, a script on the page, a page-list address, or a browser. If the page needs a browser and none is set up, it says so.
- The robots.txt verdict: allowed, disallowed, ignored (you turned robots.txt off for this source), or unreachable (robots.txt could not be read).
- Warnings, such as a page count that does not match the page's own total.

A Test and a download never run at the same time, because the app makes one request at a time to a site. Test is unavailable while a download runs, and a download waits while a Test runs.

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

- The app downloads one page at a time.
- It waits at least 5 seconds between chapters and at least 0.5 seconds between pages. The usual pauses are 5 to 10 seconds between chapters and 0.5 to 1.5 seconds between pages. A delay you set below these limits is raised to the limit, with a warning.
- If a site answers with HTTP 429 or 503 (too many requests, or busy), the whole run pauses for the time the site asks, or 60 seconds, whichever is longer. Each further pause doubles, up to 15 minutes.
- The run stops by itself, cleanly, after five pauses, if a site asks for a wait over 15 minutes, or if five images in a row fail. Run it again later. Finished chapters are not downloaded again.

## No source for a site

If you paste an address whose host matches no source, the run stops before it makes any request, with "No source profile for <host>". Add or import a source for that site under Sources.
