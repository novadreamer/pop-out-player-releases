# Privacy Policy: Pop Out Player

_Last updated: 22 November 2026_

Pop Out Player is a browser extension, with a small helper program on your PC, that opens online videos in a video
player installed on your own computer. This policy explains what it touches. In short: **it collects nothing, sends
nothing to the developer or anyone else, and keeps everything on your computer.**

## What the extension does not do
- It does not collect, sell or share any personal data.
- It has no analytics, tracking, advertising or crash reporting.
- It loads no remote code, and talks to no server of its own.
- The only requests it makes itself are to YouTube, to place its buttons on the right part of a YouTube thumbnail:
  for a YouTube video you hover, it looks up that video's public shape (4:3 or 16:9) from YouTube's oEmbed service on
  youtube.com, or reads the video's standard thumbnail image from i.ytimg.com. These requests carry only the video's
  public ID, go only to YouTube, and are made once per video while the page is open. Nothing about you is added to
  them or stored.
- It has no accounts and needs no sign-in.

## What it reads on the pages you visit
To show its buttons, the extension looks at the page under your mouse pointer: video elements, links to video pages,
and their titles. This happens only inside your browser. Normally nothing is stored or sent anywhere unless you click
**Play** or **Add to playlist**. If **Start loading a video when you point at ▶** is on and mpv is chosen, pointing at a
video's ▶ button passes that video's page address to the helper on the same computer. The helper runs your own
yt-dlp to look the video up on its site, the same request mpv makes when you click Play. The answer is kept for up to
an hour in the helper's folder under `%LOCALAPPDATA%\mpv-in-browser\prefetch`; switch this off in the popup.

When mpv is chosen, Pop Out Player also notices video stream addresses that the page's own player loads (only addresses,
read from the browser's list of what the page downloaded). They stay in the browser's session memory for that tab and
are passed only to mpv on your computer when you click Play; YouTube is not touched, and you can turn this off in the
popup.

## What it stores, and where
Using the browser's local extension storage (`chrome.storage.local`), on your computer only:
- your playlist and the playlists you save: each video's page address, title, site name and the time you added it,
  and each saved playlist's name, creation time and whether it is collapsed;
- your chosen player;
- whether the hover buttons are switched on, which side they sit on, and how My Playlists is sorted;
- whether prefetching is switched on;
- whether a player opened by the extension is still running.

You can remove playlist entries one by one or with **Clear**, and delete saved playlists in My Playlists; uninstalling
the extension deletes all of it.

## What it passes on, and to whom
When you click **Play**, the page addresses and titles of the videos to play are passed to the helper program on
the **same computer** (using the browser's "native messaging" feature). The helper starts the player you chose with
those addresses. Nothing leaves your computer at this step.

The extension also asks the helper on your own PC whether it is installed; nothing leaves the computer. In PotPlayer
basic mode, the video's address is handed to PotPlayer through Windows (a `potplayer:` link) instead of the helper.

The helper also keeps, on your computer:
- for PotPlayer or mpv with several videos, a playlist file (the videos' addresses and titles) in
  `%LOCALAPPDATA%\mpv-in-browser\playlists` (the 20 newest of each kind are kept);
- a log file (`%LOCALAPPDATA%\mpv-in-browser\host.log`, kept under about 1 MB) recording which player was started and how many videos it got. Error lines can
  include part of a rejected address.

## Third parties
- The **player** (mpv, PotPlayer, MPC-BE or MPC-HC) and the **yt-dlp** helper it uses then contact the video site
  to play the video, just as they would if you had pasted the address into them yourself. They are separate
  programs that you installed, and their own privacy terms apply, as do those of the video site.
- The **Support me on Ko-fi** button opens ko-fi.com in a new tab, only when you click it. Ko-fi's privacy policy
  applies there.

## Permissions the extension asks for
- **Read and change data on all websites**: needed to show the hover buttons on videos and thumbnails on any site.
  The extension only reads page addresses and titles, and only adds its own buttons.
- **Communicate with cooperating native applications** (`nativeMessaging`): to pass addresses to the helper on
  your PC.
- **Context menus**: to add "Play in …" and "Add to playlist" to the right-click menu.
- **Storage**: to keep your playlist and settings on your computer.

## Children
The extension is not aimed at children and collects no data from anyone.

## Changes
If this policy changes, the new version will be published here with a new date.

## Contact
Questions or concerns: through the developer's Ko-fi page, https://ko-fi.com/ashrafmustafa818.
