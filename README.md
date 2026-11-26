# Pop Out Player: helper app

Pop Out Player is a browser extension that plays the video you're watching (or a whole playlist) in a desktop
player: **mpv**, **PotPlayer**, **MPC-BE** or **MPC-HC**. Hover over a video or thumbnail and press **▶**.

This page hosts the **helper app** the extension needs. Browsers aren't allowed to start programs themselves, so the
small helper does that for them. It's needed for mpv, MPC-BE, MPC-HC, playlists, faster opening and continuing
videos where you left off. PotPlayer also
has a basic mode that works without it.

## Install the helper
1. **[Download PopOutPlayerHelperSetup.exe](https://github.com/novadreamer/pop-out-player-releases/releases/latest/download/PopOutPlayerHelperSetup.exe)**
   (Windows 10 and 11).
2. Run it. It installs for your Windows user only (no administrator rights needed) and registers itself with
   Chrome, Edge, Brave, Chromium and Vivaldi.
3. The setup isn't code-signed yet, so Windows may show **"Windows protected your PC"**. Click
   **More info → Run anyway**.

The extension's setup page notices the helper by itself within a couple of seconds, with no browser restart.

To remove it, uninstall **Pop Out Player Helper** in Windows **Settings → Apps**.

## Load the extension in developer mode (optional)
Most people should install Pop Out Player from the Chrome Web Store, which keeps it updated. If you'd rather load it
yourself (to try a version before it reaches the store, or to keep an older one):
1. **[Download PopOutPlayerExtension.zip](https://github.com/novadreamer/pop-out-player-releases/releases/latest/download/PopOutPlayerExtension.zip)**
   (the latest version; earlier versions are under [Releases](https://github.com/novadreamer/pop-out-player-releases/releases)).
2. Extract it into a folder you'll keep (the browser loads the extension from that folder every time it starts).
3. Open `chrome://extensions` (`edge://extensions`, `brave://extensions`, …), turn on **Developer mode**, click
   **Load unpacked** and choose the extracted folder (the one with `manifest.json` in it).

A copy loaded this way doesn't update itself: to update, download the new zip, replace the folder's contents and
click the extension's reload ↻ button. It works with the same helper app. Don't keep it switched on together with
the store version, or every video gets two sets of buttons.

## Your player needs yt-dlp
The helper doesn't include a player or yt-dlp (the tool players use to open YouTube and other web pages). mpv-lazy,
recent MPC-BE installers and PotPlayer's yt-dlp extension come with it; for anything else see
**[Player setup](PLAYER-SETUP.md)**.

## Continue where you left off, and video quality
Both are new in 3.10 and set in the extension's toolbar popup. They need helper 3.10 or newer; with an older helper
the popup asks you to update it.
- **Continue where you left off**: how far you watched a video, on its page or in mpv, is remembered on your PC and
  used the next time you play it, also from a playlist. In mpv every video of a playlist continues from its own point;
  PotPlayer, MPC-BE and MPC-HC continue only the first one, and only time watched on the page counts for them (they
  can't report their position). A video watched to the end starts from the beginning next time.
- **Video quality** (mpv only): **Automatic** leaves it to mpv's own settings, **Best** asks for the highest
  available, or pick a limit from 4K down to 480p. For the other players, see
  [Player setup → Video quality](PLAYER-SETUP.md#video-quality).

## Settings
The helper finds your players by itself, and if one is somewhere unusual, the setup page's **Choose…** button
saves its location for you. Create a `config.json` only if you need to change something else; every key is optional. Put it in
**`%LOCALAPPDATA%\mpv-in-browser\config.json`** (paste `%LOCALAPPDATA%\mpv-in-browser` into the Explorer address bar). Example:
```json
{ "mpv_path": "D:\\Apps\\mpv\\mpv.exe", "mpv_extra_args": ["--fs"] }
```
| Key | Default | Meaning |
|---|---|---|
| `mpv_path` | found automatically (`C:\mpv-lazy`, Program Files, Scoop, winget, Chocolatey, PATH…) | Where mpv is. The setup page's **Choose…** button sets this for you. |
| `mpv_extra_args` | `[]` | Extra mpv options, e.g. `["--fs"]`. |
| `mpv_prefetch` | `true` | Resolve a video in the background once the pointer reaches its ▶ button, so mpv opens it sooner. |
| `ytdl_real_path` | `null` | Real `yt-dlp.exe` to use for prefetching; `null` finds it the way mpv does. The helper sets mpv's `ytdl_hook-ytdl_path` to its own small stand-in, which hands over to the real yt-dlp. |
| `mpv_window_at_once` | `true` | Open mpv's window straight away, showing "Loading video…", instead of only once the video is ready; if a video can't be played, the window says so (rather than mpv waiting hidden in the background). |
| `pot_path` | found automatically | Where PotPlayer is. The setup page's **Choose…** button sets this for you. |
| `pot_extra_args` | `[]` | Extra PotPlayer options. |
| `pot_run_as_invoker` | `true` | Start PotPlayer without the "Run as administrator" prompt (for that launch only; no setting is changed). |
| `pot_new_window` | `true` | Open in a new PotPlayer window instead of handing the link to one already open. |
| `mpcbe_path` | found automatically | Where MPC-BE is. The setup page's **Choose…** button sets this for you. |
| `mpcbe_extra_args` / `mpcbe_new_window` | `[]` / `true` | As above. |
| `mpchc_path` | found automatically (including K-Lite's copy) | Where MPC-HC is. The setup page's **Choose…** button sets this for you. |
| `mpchc_extra_args` / `mpchc_new_window` / `mpchc_run_as_invoker` | `[]` / `true` / `true` | As above. |

Changes apply the next time you click Play.

## Troubleshooting
- **The extension says the helper is missing**: run the setup again, then return to the browser tab.
- **"… wasn't found"**: click **Choose…** on the setup page and pick the player's .exe; [Settings](#settings) is the
  fallback.
- **The player opens but the video doesn't play**: open the same page address directly in the player. If it fails
  there too, update yt-dlp or check the player's setup: [Player setup](PLAYER-SETUP.md).
- **"… is still open"**: Pop Out Player plays one player at a time; close the player it opened first.
- **A video doesn't continue where you left off**: check that **Continue where you left off** is on in the popup and
  that the helper is 3.10 or newer. Videos shorter than 30 seconds, live streams, and a video you watched for less
  than 5 seconds aren't remembered.

Problems or ideas: [open an issue](https://github.com/novadreamer/pop-out-player-releases/issues).

[Privacy](PRIVACY.md) · [Legal](LEGAL.md)
