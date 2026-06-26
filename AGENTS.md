# AGENTS.md

A [Hugo](https://gohugo.io/) port of the [Researcher](https://github.com/ankitsultana/researcher)
Jekyll theme.

## Styles

CSS is **precompiled and committed**: `assets/css/main.css` is generated from the SCSS in
`assets/scss/` by `npm run build:css`, and the templates load that committed file directly via
`resources.Get` — there is no SCSS transpilation at Hugo build time (Hugo's deprecated LibSass path
was dropped).

After editing any `*.scss`, run `npm run build:css` and commit the regenerated `main.css` in the
same change, or the rendered site won't reflect your edits.

## Formatting

[Prettier](https://prettier.io/) formats **Markdown, SCSS, YAML, and JSON only**. Its version is
pinned exactly in `package.json` and locked via `package-lock.json`.

- Install once with `npm ci`, then run `npm run format` after editing those files
  (`npm run format:check` verifies without writing). Node is assumed available.
- There is no CI formatting gate — formatting is enforced manually by the maintainer.
- **Hugo templates (`*.html`) are not formatted by Prettier.** Its Go-template handling mangles
  whitespace that is significant inside attribute values (e.g. a conditional CSS class). They are
  hand-authored — keep them tidy by hand.
- **TOML (`*.toml`) is not formatted by Prettier** — use [taplo](https://taplo.tamasfe.dev/).
- **The generated `assets/css/main.css` is not formatted** — it is build output (see Styles).

`*.html`, `*.toml`, and the generated `main.css` are all listed in `.prettierignore`.

## Tooling

`mise.toml` is intentionally **not** committed (personal preference). The required Hugo version is
documented in the README — do not re-add `mise.toml` to version control.

## Divergences from the original

`docs/changes-from-original.md` is a ledger of how this port intentionally differs from the upstream
Researcher Jekyll theme (new features, changed defaults, dropped options, the committed-CSS build).
When a change makes the theme behave differently from the original — not a routine bug fix or an
internal refactor that preserves behavior — add an entry there in the same change, alongside the
`CHANGELOG.md` entry, noting the version it lands in.

## Releasing

`CHANGELOG.md` follows [Keep a Changelog](https://keepachangelog.com/) and releases are tagged with
[Semantic Versioning](https://semver.org/) (`vX.Y.Z`). As you make user-facing changes, add entries
under the `## [Unreleased]` heading. To cut a release:

1. Rename `## [Unreleased]` to `## [X.Y.Z] - YYYY-MM-DD`, then add a fresh empty `## [Unreleased]`
   above it.
2. Update the compare links at the bottom of `CHANGELOG.md`.
3. Bump `version` in `package.json` to match.
4. Commit as `chore(release): vX.Y.Z`, then tag `vX.Y.Z`.
