# Development

Styles are authored in SCSS under `assets/scss/` and **precompiled** to the committed
`assets/css/main.css`. Site builds serve that file directly and never transpile SCSS — so the theme
needs no Sass toolchain and not Hugo's _extended_ edition.

The pinned [Dart Sass](https://sass-lang.com/dart-sass/) lives in `package.json`. After editing any
SCSS, regenerate and commit the CSS:

```sh
npm ci             # one-time: install the pinned toolchain
npm run build:css  # regenerate assets/css/main.css from assets/scss/main.scss
```

Commit the regenerated `assets/css/main.css` alongside your SCSS changes.
