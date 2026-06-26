# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.5.0] - 2026-06-26

### Added

- Optional `params.google_site_verification` renders a
  `<meta name="google-site-verification">` tag for Google Search Console
  ownership verification.

## [0.4.0] - 2026-06-25

### Added

- Inline and fenced code blocks now have dedicated Hugo-port styling, which was
  not part of the initial Researcher theme. It uses a light palette matching the
  theme's white/grey surfaces; the example site sets a light Chroma highlighting
  style (`style = "github"`) so syntax-highlighted blocks stay on-theme.

## [0.3.0] - 2026-06-24

### Changed

- Footer renders whenever `params.footer_text` is set; `params.footer_url` is now
  optional and falls back to plain text when omitted.
- Example site footer shortened to "Built with hugo-researcher" (the original
  Researcher theme attribution remains in the README's License section).

### Removed

- The `params.footer` boolean is no longer read — footer visibility is driven by
  whether `footer_text` is set. Existing `footer = true` lines are harmlessly
  ignored. Note: a site that set `footer_text` while leaving `footer = false` will
  now show the footer.

## [0.2.0] - 2026-06-24

### Added

- Explicit `keywords` (front matter or param) now overrides the automatic keyword
  fallback instead of being merged with it.

### Fixed

- License section in the README no longer renders as two stray bullets.

## [0.1.0] - 2026-06-24

### Added

- Initial Hugo port of the [Researcher](https://github.com/ankitsultana/researcher)
  Jekyll theme by Ankit Sultana, including the circular profile picture, optional
  institute logo, and configurable footer / analytics / social metadata.

### Build

- SCSS is precompiled to committed CSS and the deprecated LibSass path is dropped.

[unreleased]: https://github.com/yilinfang/hugo-researcher/compare/v0.5.0...HEAD
[0.5.0]: https://github.com/yilinfang/hugo-researcher/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/yilinfang/hugo-researcher/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/yilinfang/hugo-researcher/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/yilinfang/hugo-researcher/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/yilinfang/hugo-researcher/releases/tag/v0.1.0
