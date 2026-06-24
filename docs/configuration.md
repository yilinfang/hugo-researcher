# Configuration

Mirror of the original theme's `_config.yml`, expressed as Hugo `[params]` and a `[[menu.main]]`
navigation. Key options (all optional unless noted):

| Param                                                                    | Purpose                                           |
| ------------------------------------------------------------------------ | ------------------------------------------------- |
| `title` (site)                                                           | Author name shown in the navbar                   |
| `params.author`                                                          | `<meta name="author">` and keywords               |
| `params.description`                                                     | Default meta/OG description                       |
| `params.profile_picture`                                                 | Fallback image for OG / Twitter cards             |
| `params.footer` / `footer_url` / `footer_text`                           | Footer line (set `footer = true` to show)         |
| `params.ins_logo`                                                        | Optional institute logo centered above the navbar |
| `params.tracking_id`                                                     | Google Analytics (gtag) measurement id            |
| `params.favicon`                                                         | Favicon path                                      |
| `params.og_image` / `twitter_image` / `twitter_username` / `facebook_id` | Social metadata                                   |

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

## Customization

The accent (hyperlink) color and sizing live in `../assets/scss/_vars.scss` (`$accent`, `$image-size`, …).

> **Note:** Styles are transpiled with the embedded LibSass, which Hugo deprecates in favor of Dart
> Sass. The build works as-is (with a one-line deprecation notice). To silence it, install Dart Sass
> and change `transpiler "libsass"` → `"dartsass"` in `../layouts/partials/head.html`.
