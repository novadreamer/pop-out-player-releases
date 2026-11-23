# Pop Out Player: helper app

Pop Out Player is a browser extension that plays the video you're watching (or a whole playlist) in a desktop
player: **mpv**, **PotPlayer**, **MPC-BE** or **MPC-HC**. Hover over a video or thumbnail and press **▶**.

This page hosts the **helper app** the extension needs. Browsers aren't allowed to start programs themselves, so the
small helper does that for them. It's needed for mpv, MPC-BE, MPC-HC, playlists and faster opening. PotPlayer also
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

## Your player needs yt-dlp
The helper doesn't include a player or yt-dlp (the tool players use to open YouTube and other web pages). mpv-lazy,
recent MPC-BE installers and PotPlayer's yt-dlp extension come with it; for anything else see
**[Player setup](PLAYER-SETUP.md)**.

## Settings
Create a `config.json` only if you need to change something; every key is optional. Put it in
**`%LOCALAPPDATA%\mpv-in-browser\config.json`** (paste `%LOCALAPPDATA%\mpv-in-browser` into the Explorer address bar). Example:
```json
{ "mpv_path": "D:\\Apps\\mpv\\mpv.exe", "mpv_extra_args": ["--fs"] }
```
| Key | Default | Meaning |
|---|---|---|
| `mpv_path` | `C:\mpv-lazy\mpv.exe` | Where mpv is. |
| `mpv_extra_args` | `[]` | Extra mpv options, e.g. `["--fs"]`. |
| `mpv_prefetch` | `true` | Resolve a video in the background once the pointer reaches its ▶ button, so mpv opens it sooner. |
| `ytdl_real_path` | `null` | Real `yt-dlp.exe` to use for prefetching; `null` finds it the way mpv does. The helper sets mpv's `ytdl_hook-ytdl_path` to its own small stand-in, which hands over to the real yt-dlp. |
| `mpv_window_at_once` | `true` | Open mpv's window straight away, showing "Loading video…", instead of only once the video is ready; if a video can't be played, the window says so (rather than mpv waiting hidden in the background). |
| `pot_path` | `C:\Program Files\DAUM\PotPlayer\PotPlayerMini64.exe` | Where PotPlayer is. |
| `pot_extra_args` | `[]` | Extra PotPlayer options. |
| `pot_run_as_invoker` | `true` | Start PotPlayer without the "Run as administrator" prompt (for that launch only; no setting is changed). |
| `pot_new_window` | `true` | Open in a new PotPlayer window instead of handing the link to one already open. |
| `mpcbe_path` | `C:\Program Files\MPC-BE\mpc-be64.exe` | Where MPC-BE is. |
| `mpcbe_extra_args` / `mpcbe_new_window` | `[]` / `true` | As above. |
| `mpchc_path` | standard MPC-HC or K-Lite location | Where MPC-HC is. |
| `mpchc_extra_args` / `mpchc_new_window` / `mpchc_run_as_invoker` | `[]` / `true` / `true` | As above. |

Changes apply the next time you click Play.

## Troubleshooting
- **The extension says the helper is missing**: run the setup again, then return to the browser tab.
- **"… was not found at …"**: the player isn't in its standard folder; set its path in [Settings](#settings).
- **The player opens but the video doesn't play**: open the same page address directly in the player. If it fails
  there too, update yt-dlp or check the player's setup: [Player setup](PLAYER-SETUP.md).
- **"… is still open"**: Pop Out Player plays one player at a time; close the player it opened first.

Problems or ideas: [open an issue](https://github.com/novadreamer/pop-out-player-releases/issues).

[Privacy](PRIVACY.md) · [Legal](LEGAL.md)
