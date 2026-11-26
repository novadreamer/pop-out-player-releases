# Setting up the players

Pop Out Player hands each player the **page address** of a video (for example `https://www.youtube.com/watch?v=…`),
exactly as if you had pasted it in. The player then needs a helper that turns a page address into the actual video
stream. For almost every player that helper is **yt-dlp**, and for YouTube yt-dlp in turn needs **Deno** (a
JavaScript runtime it uses to read YouTube's player code).

| Player | Where `yt-dlp.exe` goes | Where `deno.exe` goes | Included already? |
|---|---|---|---|
| mpv (mpv-lazy) | next to `mpv.exe` | next to `mpv.exe` | Yes, both |
| mpv (plain build) | next to `mpv.exe`, or on your `PATH` | same place as yt-dlp | No |
| PotPlayer | `PotPlayer\Module\` (**not** the main folder) | `PotPlayer\Module\` | Often, see below |
| MPC-BE | MPC-BE's main folder | MPC-BE's main folder | Yes in recent versions |
| MPC-HC | MPC-HC's main folder | MPC-HC's main folder | No |

You only need to set up the players you will actually use.

## Getting the files
- **yt-dlp**: these links download `yt-dlp.exe` itself (keep that name), then put it where the table above says:
  - **[Stable `yt-dlp.exe`](https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp.exe)**: take this one.
  - **[Nightly `yt-dlp.exe`](https://github.com/yt-dlp/yt-dlp-nightly-builds/releases/latest/download/yt-dlp.exe)**:
    built every day with the newest site fixes. If a site stops working with Stable, download this over it.

  On the [releases page](https://github.com/yt-dlp/yt-dlp/releases/latest) the file you want is `yt-dlp.exe`; the
  others (`yt-dlp_x86.exe`, `yt-dlp_win.zip`, the one named just `yt-dlp`, …) are builds you don't need.
- **Deno**: download `deno-x86_64-pc-windows-msvc.zip` from the
  [Deno releases page](https://github.com/denoland/deno/releases/latest) and take `deno.exe` out of it.

Copying into `C:\Program Files\…` asks for administrator permission; that is normal.

**Keep yt-dlp up to date.** Video sites change often, and an old yt-dlp is the most common reason a video stops
playing. Download a new `yt-dlp.exe` over the old one, or run `yt-dlp.exe -U` from its folder (from an
administrator terminal if it is under `Program Files`). PotPlayer's yt-dlp extension can also offer the update
itself.

## mpv
- **mpv-lazy** (the default path is `C:\mpv-lazy\mpv.exe`) already ships `yt-dlp.exe` and `deno.exe` beside
  `mpv.exe`. Nothing to add.
- **A plain mpv build**: put `yt-dlp.exe` and `deno.exe` next to `mpv.exe` (mpv's built-in yt-dlp support looks
  there first, then on `PATH`).
- mpv is found automatically in the usual install folders. If it is somewhere else, use **Choose…** on the setup
  page; the settings file is the fallback (see [Settings](README.md#settings)).
- Several videos open as mpv's own playlist; mpv's usual keys move between them (`<` and `>` by default).

## Video quality

The popup's **Video quality** setting applies to **mpv**: **Automatic** (the default) leaves the choice to mpv and its
own settings; **Best** asks for the highest available; or pick a limit from 4K down to 480p. It works both when it
resolves a page through yt-dlp and when it plays the site's own HLS stream. With a limit, mpv takes the highest
quality available up to it (a video with nothing that small still plays).

The other players keep their own quality setting, so set it there once:
- **MPC-BE**: **Options → Online Services**, the yt-dlp maximum resolution.
- **MPC-HC**: **Options → Advanced → `YDLMaxHeight`**.
- **PotPlayer**: its YouTube and yt-dlp extensions offer the site's qualities to PotPlayer; choose the quality in
  PotPlayer itself.

## PotPlayer (special case)
PotPlayer does not call yt-dlp by itself. It handles web addresses through **extensions**, listed in
**Preferences (F5) → Extensions → Media Playback**:

- **YouTube** (`MediaPlayParse - YouTube`): PotPlayer's own built-in YouTube support. It needs no yt-dlp at all
  and handles YouTube links on its own.
- **yt-dlp** (`MediaPlayParse - yt-dlp`): a separate extension that uses yt-dlp, which is what makes other sites
  play in PotPlayer. Recent PotPlayer versions include
  it; otherwise it comes from [PotPlayer-Extension_yt-dlp](https://github.com/hgcat-360/PotPlayer-Extension_yt-dlp).

Setup:
1. Put `yt-dlp.exe` and `deno.exe` in **`C:\Program Files\DAUM\PotPlayer\Module\`**. The yt-dlp extension
   only looks in the `Module` folder; a copy in PotPlayer's main folder is ignored.
2. Make sure both extensions are enabled in **Extensions → Media Playback**.
3. Choose who plays YouTube. When two extensions can handle the same link, the one **higher in the list** gets it
   first. If the built-in **YouTube** extension is above **yt-dlp**, PotPlayer's own YouTube support is used;
   move yt-dlp above it if you prefer yt-dlp (for example, if YouTube plays at a low quality or fails with the
   built-in one). The yt-dlp extension's `enable_youtube` setting fine-tunes this.
4. To change the yt-dlp extension's settings, edit
   `%APPDATA%\PotPlayerMini64\Extension\Media\PlayParse\yt-dlp.ini`. Do **not** edit `yt-dlp_default.ini` in
   the program folder; it is replaced on updates.

Other PotPlayer notes:
- `PotPlayerMini64.exe` is often marked "Run as administrator". Pop Out Player starts it normally for that one
  launch instead (no setting is changed), so no permission prompt appears.
- Several videos are handed over as a PotPlayer playlist file (`.dpl`, with titles), saved in
  `%LOCALAPPDATA%\mpv-in-browser\playlists` (the 20 newest are kept).

## MPC-BE
- Recent MPC-BE installers include `yt-dlp.exe` and `deno.exe` in the program folder
  (`C:\Program Files\MPC-BE\`). If yours does not, copy them in.
- Several videos open as MPC-BE's own playlist in a new window.
- MPC-BE is found automatically in the usual install folders. If it is somewhere else, use **Choose…** on the setup
  page; the settings file is the fallback (see [Settings](README.md#settings)).

## MPC-HC
- Copy `yt-dlp.exe` and `deno.exe` into MPC-HC's program folder (for example `C:\Program Files\MPC-HC\`, or
  `C:\Program Files (x86)\K-Lite Codec Pack\MPC-HC64\` for the K-Lite copy).
- In **Options → Advanced**, `UseYDL` must be `true` (the default). `YDLMaxHeight` sets the highest quality it
  picks.
- Pop Out Player finds MPC-HC in its usual standalone and K-Lite locations. If it is somewhere else, use **Choose…**
  on the setup page; the settings file is the fallback.

## Checking a player on its own
If a video will not play from Pop Out Player, paste the same page address into the player directly (in most players,
**Open → Open URL**, or `Ctrl+U`). If it fails there too, the problem is the player's yt-dlp setup above, not the
extension. Remember that DRM-protected (copy-protected) video from paid streaming services cannot play in any of
these players.
