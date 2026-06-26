# Changes from the original theme

A running record of how this Hugo port **intentionally diverges** from the upstream
[Researcher](https://github.com/ankitsultana/researcher) Jekyll theme by Ankit Sultana — new
features, behavioral differences, and the build-process decision.

This is the divergence ledger: when you add a feature the original lacks, or change a behavior it
defined, record it here (see [Maintaining this page](#maintaining-this-page)). Pure Jekyll → Hugo
translation that preserves the original's behavior (config format, URL handling, etc.) is summarized
under [Porting mechanics](#porting-mechanics) rather than logged item-by-item. Each entry notes the
version it landed in, mirroring `CHANGELOG.md`.

## Additions (not in the original)

- **Inline & fenced code-block styling** _(since v0.4.0)_ — dedicated styling with a light palette
  matching the theme's white/grey surfaces. The original had no code-block treatment. The example
  site sets a light Chroma highlighting style (`style = "github"`) so syntax-highlighted blocks stay
  on-theme. See `docs/configuration.md` → _Code blocks_.
- **Google Search Console verification** _(since v0.5.0)_ — optional
  `params.google_site_verification` renders a `<meta name="google-site-verification">` tag in the
  `<head>` (`layouts/partials/head.html`). Off by default.

## Behavioral changes (differs from the original)

- **Footer visibility** _(since v0.3.0)_ — the footer renders whenever `params.footer_text` is set;
  the original's `footer` boolean was dropped, and `params.footer_url` is now optional (plain text
  when omitted). A site that set `footer_text` while leaving `footer = false` will now show the
  footer. See `layouts/partials/footer.html`.
- **Keywords override** _(since v0.2.0)_ — explicit keywords (`params.keywords` or a page's
  front-matter `keywords`) replace the automatic `researcher` / author / title / `hugo` fallback
  entirely, instead of merging with it. See `layouts/partials/head.html`.

## Build & tooling

- **Precompiled, committed CSS** _(since v0.1.0)_ — SCSS in `assets/scss/` is precompiled to the
  committed `assets/css/main.css` and served directly via `resources.Get`; there is no SCSS
  transpilation at Hugo build time and the deprecated LibSass path was dropped. Consequently,
  **building a site with this theme needs no Sass toolchain and not Hugo's _extended_ edition**.
  Editing styles is a maintainer workflow (`npm run build:css`) — see `docs/development.md`.

## Porting mechanics

Expected Jekyll → Hugo translations that keep the original's behavior. Full details live in
`docs/configuration.md`; summarized here for orientation:

- **Configuration** — the original's `_config.yml` becomes Hugo `[params]` plus a `[[menu.main]]`
  navigation.
- **baseURL** — Jekyll's separate `url` (host) + `baseurl` (subpath) become a single Hugo `baseURL`.
- **New-tab links** — the original special-cased the "Resume" entry to open in a new tab; here any
  menu entry can set `newtab = true` (`layouts/partials/header.html`).
- **Profile picture** — provided as the `{{</* profile-picture src="…" alt="…" */>}}` shortcode
  (`layouts/shortcodes/profile-picture.html`); raw `<img class="profile-picture">` still works when
  `markup.goldmark.renderer.unsafe = true` (set in the example site for kramdown parity).
- **Single-page kinds** — the example site sets `disableKinds = ["taxonomy", "term"]` to match the
  original's single-page résumé (no tags/categories).

## Maintaining this page

When a change makes this port behave differently from the original Researcher theme — a new feature,
a changed default, a dropped option — add it here in the same change, alongside the `CHANGELOG.md`
entry. Note the version it lands in. Routine bug fixes and internal refactors that preserve the
original's behavior do not belong here.
