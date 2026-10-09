# HotMic marketing site

Static site for HotMic for Mac (`index.html`, `privacy.html`, `eula.html`,
`google-meet-airpods.html`). Plain HTML/CSS, no build step, no external
origins except Paddle.js for checkout. It works opened straight from `file://` and hosted on GitHub Pages.

> ## Domain: registered, not serving yet
>
> `CNAME` in this repo points at **usehotmic.com**. The domain is registered
> (Amazon Registrar, hosted zone in Route 53) but is **not serving yet**: the
> GitHub Pages DNS records below still have to be added. The domain is also
> the planned Sparkle `SUFeedURL` host (see "Where the appcast will live").
> Once a build ships with it, don't change it.

## Publishing

Published at github.com/mikaelq/hotmic-site (public; GitHub Pages on a free
account requires that). Pages deploys `main` from the repo root.

## GitHub Pages setup

1. `usehotmic.com` is already registered (Amazon Registrar / Route 53).
   Optionally register `hotmicformac.com` as a redirect.
2. Pushed; Pages deploys from `main`, root (done).
3. In the Route 53 hosted zone for `usehotmic.com`, add four A records for
   the apex:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. Add a `CNAME` DNS record for `www` pointing to `mikaelq.github.io`.
5. Back in Settings → Pages, confirm the custom domain shows `usehotmic.com`
   (the `CNAME` file in this repo pre-fills it) and, once the DNS check
   passes, tick **Enforce HTTPS**.

## Assets

`assets/` holds the brand images, generated from the product repo's
`Design/Brand/` and `HotMic/AppIcon.icon/` sources plus the Duck Duck Grey
Duck LLC logo:

- `glyph-56.png`, `glyph-84.png`: header glyph at 2x and 3x (from the app
  icon's `glyph-dark.png` layer).
- `favicon.ico`, `favicon-16.png`, `favicon-32.png`, `apple-touch-icon.png`:
  the glyph on the app icon's `#fbfbfc` tile.
- `og-image.png` (1200x630): link-preview image. Pages reference it by
  absolute URL (`https://usehotmic.com/assets/og-image.png`), so previews
  stay empty until the domain is serving.
- `ddgd-logo-360/540.{png,webp}`: Duck Duck Grey Duck LLC logo for the
  footer credit, white background removed. It only works on light
  backgrounds.

## Where the appcast will live

The Sparkle update feed and release archives will be served from this same
Pages site, under `appcast/`:

- `https://usehotmic.com/appcast/appcast.xml`: this is the `SUFeedURL` to
  set in the product repo's `project.yml` (it is baked into every shipped
  build; changing it later means serving the old URL forever).
- `https://usehotmic.com/appcast/HotMic-<version>.zip`: the update archives
  referenced by the appcast (`Scripts/release.sh` in the product repo emits
  `dist/appcast.xml` + zips; copy them into `appcast/` here).
- `https://usehotmic.com/appcast/revoked-keys.txt`: the signed revoked-key
  list the app downloads after each update check. Maintained with
  `LicenseWorker/scripts/revoke-key.js` in the product repo; publish it
  whenever you revoke a key (refunds, leaked keys). No file is fine until
  the first revocation.

## Placeholders still to fill before launch

- Both download buttons in `index.html` (`href="#"`) → the GitHub Releases
  DMG URL.
- The three buy buttons in `index.html` (`href="#"`) → Paddle.js checkout
  wiring; the live Paddle price IDs are already on the buttons as
  `data-paddle-price-id`.
- `eula.html` is a DRAFT (visible banner): `[DATE]` and the governing law /
  venue (`[JURISDICTION]`, `[VENUE]`, §11.1) are unfilled, attorney review
  pending. The Licensor is Duck Duck Grey Duck LLC.
- support@usehotmic.com must receive mail before launch.

## Rules for this site

No analytics, no cookies of our own, and no external scripts, fonts, or
other third-party origins, except Paddle.js for the overlay checkout
(and the cookies Paddle sets for it). The privacy page and the home
page privacy band say exactly this; keep them true.
