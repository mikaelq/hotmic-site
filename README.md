# HotMic marketing site

Static one-pager for HotMic for Mac (`index.html`, `privacy.html`,
`eula.html`). Plain HTML/CSS, no build step, no external origins — it works
opened straight from `file://` and hosted on GitHub Pages.

> ## ⚠️ Domain is NOT registered yet
>
> `CNAME` in this repo points at **usehotmic.com**, which is the
> *recommended* domain (verified available 2026-09-21) but is **still
> unregistered**. Availability is not reserved — **register usehotmic.com
> BEFORE pushing this repo or configuring Pages**. Publishing a CNAME for a
> domain you don't own invites hijacking, and the domain also becomes the
> Sparkle `SUFeedURL` baked into every shipped build, so it must be settled
> first.

## Publishing (left for the owner to run)

Nothing here has been pushed. When ready:

```sh
gh repo create hotmic-site --public --source . --push
```

Note: GitHub Pages on a free account requires a **public** repo.

## GitHub Pages setup

1. Register `usehotmic.com` (and optionally `hotmicformac.com` as a
   redirect).
2. Push this repo (command above).
3. Repo → Settings → Pages → "Deploy from a branch" → branch `main`, folder
   `/ (root)`.
4. At your DNS provider, for the apex `usehotmic.com`, add four A records:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
5. Add a `CNAME` DNS record for `www` pointing to `<your-github-username>.github.io`.
6. Back in Settings → Pages, confirm the custom domain shows `usehotmic.com`
   (the `CNAME` file in this repo pre-fills it) and, once the DNS check
   passes, tick **Enforce HTTPS**.

## Where the appcast will live

The Sparkle update feed and release archives will be served from this same
Pages site, under `appcast/`:

- `https://usehotmic.com/appcast/appcast.xml` — this is the `SUFeedURL` to
  set in the product repo's `project.yml` (it is baked into every shipped
  build; changing it later means serving the old URL forever).
- `https://usehotmic.com/appcast/HotMic-<version>.zip` — the update archives
  referenced by the appcast (`Scripts/release.sh` in the product repo emits
  `dist/appcast.xml` + zips; copy them into `appcast/` here).

## Placeholders still to fill before launch

- Both download buttons in `index.html` (`href="#"`) → the GitHub Releases
  DMG URL.
- The three buy buttons in `index.html` (`href="#"`) → Paddle.js checkout
  wiring; the live Paddle price IDs are already on the buttons as
  `data-paddle-price-id`.
- `[SUPPORT EMAIL]` in `privacy.html` and `eula.html`.
- `eula.html` is a DRAFT (visible banner): bracketed placeholders unfilled,
  attorney review pending.

## Rules for this site

No analytics, no cookies, no external scripts, fonts, or any other
third-party origins. The privacy page says so; keep it true.
