# Configuration

Mirror of the original theme's `_config.yml`, expressed as Hugo `[params]` and a `[[menu.main]]`
navigation. Key options (all optional unless noted):

| Param                                                                    | Purpose                                                  |
| ------------------------------------------------------------------------ | -------------------------------------------------------- |
| `title` (site)                                                           | Author name shown in the navbar                          |
| `params.author`                                                          | `<meta name="author">` (and the keyword fallback)        |
| `params.keywords`                                                        | Explicit `<meta name="keywords">`, replaces the fallback |
| `params.description`                                                     | Default meta/OG description                              |
| `params.profile_picture`                                                 | Fallback image for OG / Twitter cards                    |
| `params.footer_text` / `footer_url`                                      | Footer line; shown when `footer_text` set; link optional |
| `params.ins_logo`                                                        | Optional institute logo centered above the navbar        |
| `params.tracking_id`                                                     | Google Analytics (gtag) measurement id                   |
| `params.favicon`                                                         | Favicon path                                             |
| `params.og_image` / `twitter_image` / `twitter_username` / `facebook_id` | Social metadata                                          |

Navigation is a standard Hugo menu. Add `newtab = true` to a menu entry's params to open it in a
new tab (used for the Resume PDF):

```toml
[[menu.main]]
name = "Resume"
url = "/resume.pdf"
weight = 20
[menu.main.params]
newtab = true
```

## baseURL note (Jekyll → Hugo)

Jekyll split `url` (host) and `baseurl` (subpath). Hugo uses a single `baseURL` that includes the
subpath. Deploying at a domain root → `baseURL = "https://example.com/"`; deploying under a
subdirectory → `baseURL = "https://example.com/researcher/"`. All theme links use relative/absolute
URL helpers, so paths resolve correctly either way.

## Content conventions

- **Home page:** `content/_index.md` — leave the title empty so the `<title>` falls back to the site title.
- **Profile picture:** use the shortcode `{{</* profile-picture src="/sherlock.jpg" alt="…" */>}}`.
  (Raw `<img class="profile-picture">` HTML also works if `markup.goldmark.renderer.unsafe = true`.)
- **Publications / references:** ordered markdown lists (`1.` `2.`) render as `[1]`, `[2]` automatically.
- **Contact-style pages:** set `is_contact: true` in front matter to apply the contact content class.
- **Code blocks:** inline and fenced code are styled for the theme's light palette. Syntax-highlighting
  colors come from Hugo's Chroma highlighter as inline styles, so the theme's CSS can't recolor them —
  pick a **light** highlighting style in your site config to match (Hugo's default `monokai` is dark).
  The example site uses:

  ```toml
  [markup.highlight]
  style = "github" # or friendly, pastie, …
  ```

- **Per-page keywords:** add `keywords: ["…", "…"]` to a page's front matter to set or extend its
  `<meta name="keywords">`. Any explicit keywords — here or in `params.keywords` — replace the automatic
  `researcher` / author / title / `hugo` fallback entirely.

## Customization

The accent (hyperlink) color and sizing live in `../assets/scss/_vars.scss` (`$accent`, `$image-size`, …).
Because styles are **precompiled** to the committed `../assets/css/main.css`, changing them means
editing the SCSS and regenerating that file with `npm run build:css` (see [Development](development.md)).
If you consume the theme as a Hugo Module, override the styles with your own CSS instead.

> **Note:** Building a site with this theme needs **no Sass toolchain** (neither LibSass nor Dart Sass)
> and **not** Hugo's _extended_ edition — the committed `../assets/css/main.css` is served directly,
> fingerprinted with Subresource-Integrity.
