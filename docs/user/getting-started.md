# Getting started

The first time you open Manga desk it walks you through five steps. You can skip any step after Welcome and do it later from Settings, or choose Run the first-launch steps again in Settings › About. Skipping the phone and the sources still leaves Library, Jobs, Storage and Settings working.

## The five steps

### 1. Welcome

The welcome step shows a short note about what the app is for: Manga desk ships no content and no list of websites, and you should only add sources and download material you have the right to copy. You confirm that you have read it. The app stores the date and time of your confirmation.

The same stance is in the [Terms](../legal/terms.md), which Settings › About links.

### 2. Library folder

Choose the folder where Manga desk keeps your manga. The default is:

- macOS: a folder named `Manga desk` in your home folder.
- Windows: a folder named `Manga desk` in your user folder (`%USERPROFILE%\Manga desk`).

Inside it the app uses two folders:

- `downloads` holds the page images the app downloads, one folder per series and chapter.
- `library` holds the `.cbz` archives built from them. This is what goes to your phone.

If you pick a folder that already has a `downloads` or `library` folder inside, the app uses what is there.

If the folder already has a `downloads` or `library` folder inside, the button reads Use existing folder.

You can change the folder later with Change… in Settings › Library folder, and open it with Show library folder there or in the Library. Changing it points the app at another folder. The app never moves your files: if you want them in the new place, copy them yourself first.

### 3. Phone (optional)

The app lists the iPhones it can see, then the apps on the chosen phone that have file sharing turned on. Inkshelf is preselected when it is installed. The full steps, including trusting the computer, are in [Set up your iPhone](./iphone.md). Do this step later with Choose iPhone… in Settings › iPhone (Change… once a phone is chosen).

### 4. Sources (optional)

A source tells the app how a website you may copy from is laid out. You can type one or import a file someone shared. Use Test to check it on one chapter address. See [Sources](./sources.md). Save or discard the source before you continue. Add sources later under Sources in the top bar.

### 5. Browser support (optional)

A few sites need a browser to show their pages. You can install a small browser for the app, use Chrome or Microsoft Edge if you already have it, or choose Not now. See [Browser support](./browser-support.md). Set it up later in Settings › Browser support.

## Which folder to choose

Pick a plain folder on your own disk. Avoid:

- iCloud Drive and OneDrive. They sync files in the background and may move them off your disk, which slows or breaks downloads and syncs.
- Desktop and Documents. They may be synced by iCloud Drive or OneDrive, and macOS asks for your permission before an app can use them.

The app warns you if you choose one of these.

## After the steps

1. Open Library and choose Add series.
2. Paste the address of the first chapter of a series from a source you set up.
3. The app downloads the chapters one page at a time. Open Jobs to watch progress or stop the job.
4. The app builds `.cbz` archives in your `library` folder.
5. Connect your phone and choose Sync to iPhone. Then open the reader app on the phone to see the new chapters.

A download you stop or that stops by itself (see [Troubleshooting](./troubleshooting.md)) is safe to run again. The app skips finished chapters and carries on from where it stopped.

To save disk space later, open Storage. It shows how much space the original page images take once archives exist, and Prune can remove those images. The `.cbz` archives stay.

## No phone?

The `library` folder works with any comic reader that opens `.cbz` files. See the manual options in [Set up your iPhone](./iphone.md).
