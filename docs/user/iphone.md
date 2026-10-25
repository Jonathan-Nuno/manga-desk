# Set up your iPhone

Manga desk copies your finished chapters into a reader app on your iPhone over a USB cable. This page covers the setup, what the app writes on the phone, and how to copy files by hand when you cannot use the cable.

## What you need

- An iPhone and a USB cable.
- A reader app on the iPhone that has file sharing turned on. Inkshelf is the suggested reader and is preselected when the app finds it. Other readers work too if they support file sharing. Only apps that have file sharing appear in the list.
- On macOS: nothing else to install.
- On Windows: Apple's Apple Devices app, free from the Microsoft Store (when Manga desk cannot reach Apple's device service, it offers Open in Microsoft Store and Copy link). iTunes also works. Windows needs the cable: the Apple Devices service does not list a phone that is only on Wi-Fi.

## Set up the phone

1. Install the reader app on the iPhone.
2. Connect the iPhone to the computer with the cable and unlock it.
3. Let the iPhone trust the computer:
   - macOS: open Finder once so that it shows the iPhone in the sidebar.
   - Windows: open the Apple Devices app once with the iPhone connected.
4. When the iPhone asks "Trust This Computer?", tap Trust and enter your passcode.
5. In Manga desk, open Settings › iPhone and choose Choose iPhone… (Change… once a phone is chosen). Choose your iPhone, then choose the reader app from the list. If the phone is not listed, choose Refresh. Open iPhone there shows the phone's state.

The app lists the phone's apps from the phone itself, so you never type a device ID or an app ID.

## Sync

1. In Manga desk, choose Sync to iPhone.
2. The dialog can show what would be copied before it writes anything. Check it, then start the sync.
3. Keep the cable connected and the iPhone unlocked until the sync ends. A phone that you have unlocked once since it started often keeps working when its screen locks, but a long sync is safer unlocked.
4. When the sync says it is done, open the reader app on the iPhone. The app cannot open apps on the phone for you, and the reader looks for new chapters when it comes back to the front.

The cable is the supported way. If the phone is on the same Wi-Fi network and Wi-Fi sync is turned on in Finder, Wi-Fi may also work on macOS, but this is best effort and slower.

## What Manga desk writes on the phone

- It writes only inside the reader app's own Documents folder, which the app shares with your computer through file sharing.
- It makes one folder per series there. The folder name is the series name as a short name made of lowercase letters, digits, dots and dashes.
- Each series folder holds the chapter `.cbz` files, the cover image and a `series.json` file that lists the chapters.
- It copies only what is missing or different. It compares the file name, the size and the modification time, and it gives each copied file the same modification time as the file in your library. So an unchanged file is not copied again.
- It writes each file under a temporary hidden name that starts with `.mdtmp-`, then renames it. If the sync is interrupted, a half-written file never has a real name. The app removes its own leftover temporary files the next time it syncs that series.
- It deletes nothing else. It does not remove files you or the reader put there, it does not remove a series you deleted from the library, and it does not touch other folders. To remove a series from the phone, delete it in the reader app or in the Files tab (see below).
- It writes no extra bookkeeping file into the reader's folder.
- After a copy it lists the series folder again and checks that every file is there with the right size.

## Copy files by hand

You can use these ways with or without Manga desk's own sync. First open your library: choose Show library folder in Manga desk, then open the `library` folder. Each series has its own folder of `.cbz` files.

### Finder (macOS)

1. Connect the iPhone and select it in the Finder sidebar.
2. Open the Files tab.
3. Drag the series folders from the `library` folder onto the reader app's name in that list.

### Apple Devices app (Windows)

1. Connect the iPhone and select it in the Apple Devices app.
2. Open Files.
3. Drag the series folders from the `library` folder onto the reader app's name in that list.

### AirDrop

Select the `.cbz` files in Finder, choose Share › AirDrop, and send them to the iPhone. On the phone, open them in the reader app. AirDrop is not available on Windows.

### Files app

Copy the `.cbz` files to a folder in iCloud Drive or on the phone, then open them from the Files app in the reader app, using the reader's own import option. Check the reader's help for the exact steps.

## Troubleshooting

See [Troubleshooting](./troubleshooting.md): phone not found, phone not trusted, phone locked, Apple Devices missing, and a reader that is not listed.
