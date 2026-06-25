# AGENTS.md

This is a [Hugo](https://gohugo.io/) port of theme [Researcher](https://github.com/ankitsultana/researcher).

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

Both `*.html` and `*.toml` are listed in `.prettierignore`.

## Tooling

`mise.toml` is intentionally **not** committed (personal preference). The required Hugo version is
documented in the README — do not re-add `mise.toml` to version control.

## Releasing

`CHANGELOG.md` follows [Keep a Changelog](https://keepachangelog.com/) and the repo is tagged with
[Semantic Versioning](https://semver.org/) (`vX.Y.Z`). As you make user-facing changes, add entries
under the `## [Unreleased]` heading. To cut a release:

1. Rename `## [Unreleased]` to `## [X.Y.Z] - YYYY-MM-DD` and add a fresh empty `## [Unreleased]`
   above it.
2. Update the compare links at the bottom of `CHANGELOG.md`.
3. Bump `version` in `package.json` to match.
4. Commit as `chore(release): vX.Y.Z`, then tag `vX.Y.Z`.
