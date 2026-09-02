# BetterTyping

An [Equicord](https://github.com/Equicord/Equicord) userplugin that tidies up your outgoing messages. It combines Equicord's built-in
[ClearURLs](https://github.com/Equicord/Equicord/tree/main/src/plugins/clearURLs) and
[PolishWording](https://github.com/Equicord/Equicord/tree/main/src/equicordplugins/polishWording) plugins into one, and adds
an embed-fixer that rewrites links to their `fx` mirrors.

## What it does

**Links**

- **Clears tracking parameters** using the live [ClearURLs rules](https://github.com/ClearURLs/Rules) (`utm_*`, Spotify `si`, Twitter `s`/`t`, ...).
  The rules also apply to links that are already on a fixer host, so `open.fxspotify.com/track/...?si=...` loses its `si` too.
- **Fixes embeds** by swapping the host for a mirror that Discord embeds properly:

  | You type | It sends |
  | --- | --- |
  | `open.spotify.com` | `open.fxspotify.com` |
  | `music.apple.com` | `open.fxapplemusic.com` |
  | `twitter.com` | `fxtwitter.com` |
  | `x.com` | `fixupx.com` |
  | `bsky.app` | `fxbsky.app` |
  | `instagram.com` | `instagramez.com` |
  | `tiktok.com`, `vm.tiktok.com`, `vt.tiktok.com` | `vxtiktok.com` |
  | `reddit.com`, `old.reddit.com` | `rxddit.com` |
  | `pixiv.net` | `phixiv.net` |
  | `tumblr.com` | `tpmblr.com` |

  Links wrapped in `<...>` (embed suppressed) are left alone. Add your own or override a default in settings with
  comma-separated `host>replacement` pairs, e.g. `x.com>fxtwitter.com`. Map a host to itself to opt out of a default.

**Wording** (all from PolishWording, each individually toggleable)

- Ensure contractions have apostrophes (`dont` -> `don't`).
- Expand contractions (`don't` -> `do not`).
- Capitalize sentences, with a blocklist of words to leave lowercase.
- Add periods to the end of sentences, with an adjustable frequency.

Code blocks and inline code are never touched. A **Quick disable** toggle turns everything off without a client reload.

```
https://open.spotify.com/track/1UR0y...?si=ad018e19   ->  https://open.fxspotify.com/track/1UR0y...
https://x.com/user/status/123?s=20&t=abc            ->  https://fixupx.com/user/status/123
<https://x.com/user/status/123>                     ->  <https://x.com/user/status/123>
```

## Install

Userplugins only work on a **dev install** of Equicord — a `git clone` of the repo built locally with Node and pnpm. The normal Equicord GUI installer ships prebuilt releases that are compiled without `src/userplugins`, so it cannot load this.

### With UserpluginInstaller

Enable the `UserpluginInstaller` plugin in Equicord, paste this repo's URL, and click Install.

### Manually

```sh
cd <your Equicord clone>/src/userplugins
git clone https://github.com/dlyrr/BetterTyping
cd ../..
pnpm build
```

Then restart Discord and enable **BetterTyping** in the plugin list.

## Credits

The link-cleaning and wording code is adapted from Equicord's ClearURLs (adryd, thororen) and PolishWording (Samwich, WKoA) plugins, under the GPL-3.0 license.
