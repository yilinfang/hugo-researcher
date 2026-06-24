# Example site

A complete, working demo of the **hugo-researcher** theme.

The theme lives in the repository root (one level above this folder), so the commands below point
Hugo at the repo's parent directory via `--themesDir ../..` to resolve `theme = "hugo-researcher"`.
Requires **Hugo extended** (see the [project README](../README.md#requirements)).

## Preview

From the repository root:

```bash
hugo server --source exampleSite --themesDir ../..
```

…or from inside this `exampleSite/` directory:

```bash
hugo server --themesDir ../..
```

Then open <http://localhost:1313/>. The server live-reloads on edits. Add `-D` to include draft
content.

## Build

```bash
hugo --source exampleSite --themesDir ../.. --minify
```

The static output is written to `exampleSite/public/`.
