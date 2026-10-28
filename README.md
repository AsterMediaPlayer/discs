# discs.astermediaplayer.com

The website for the **Disc Menus catalogue**: shareable DVD and Blu-ray style menus for Jellyfin, used by the
[Aster Disc](https://github.com/AsterMediaPlayer/aster-companion-plugins/tree/main/AsterDisc) plugin.

This repository holds no menus or site code. Its one workflow builds
[peppy6582/jellydisc-menus](https://github.com/peppy6582/jellydisc-menus) for this address and publishes it with
GitHub Pages. To add or change a menu, or to change the site, go there.

## Two addresses, on purpose

| Address | What it's for |
|---|---|
| `https://discs.astermediaplayer.com/` | The site people browse (this repository). |
| `https://peppy6582.github.io/jellydisc-menus/` | Where the catalogue's data lives. The plugin downloads menus from here, and installed menus load their artwork from here, so it must never move. It shows a banner pointing people to the new site. |

## When it rebuilds

- Right after each publish of jellydisc-menus (it sends a `catalogue-updated` dispatch; that needs the
  `DISCS_DISPATCH_TOKEN` secret there).
- Daily, as a fallback, and on demand from the Actions tab.

## Setup (once)

1. **Settings ▸ Pages:** source **GitHub Actions**, custom domain `discs.astermediaplayer.com`, then **Enforce HTTPS**
   once the certificate is ready.
2. **DNS (Cloudflare):** `CNAME discs → astermediaplayer.github.io`, **DNS only** (grey cloud), so GitHub can issue the
   certificate.
3. **In jellydisc-menus:** add a fine-grained token with **Contents: read and write** on this repository as the
   `DISCS_DISPATCH_TOKEN` Actions secret.
