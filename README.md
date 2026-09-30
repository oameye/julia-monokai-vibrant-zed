# Julia Monokai Vibrant for Zed

A dark [Zed](https://zed.dev) theme ported from
[Julia (Monokai Vibrant)](https://github.com/CameronBieganek/julia-color-themes)
by Cameron Bieganek (itself a modified version of
[Monokai Vibrant](https://github.com/dylantmarsh/monokai-vibrant) by Dylan Marsh).
Tuned for Julia, with matching Python tweaks carried over where Zed's
Tree-sitter captures allow it.

- Family: `Julia Monokai Vibrant`
- Theme: `Julia Monokai Vibrant` (dark)
- Editor background: `#16171D`, foreground: `#f8f8f0`

## What's required for a Zed theme

1. An extension repo with an `extension.toml` manifest (`id`, `name`,
   `version`, `schema_version = 1`, `authors`, `description`, `repository`).
2. A `themes/` directory with one or more theme files. Each file is a
   Theme Family object (`name`, `author`, `themes[]`) conforming to
   https://zed.dev/schema/themes/v0.2.0.json.
3. Each theme sets `name`, `appearance` (`"dark"` here), and a `style`
   object (UI colors, `syntax` captures, terminal ANSI colors).

No Rust/WASM is needed for a theme-only extension.

## Use it now (local install)

```sh
cp themes/julia-monokai-vibrant.json ~/.config/zed/themes/
```

Then restart Zed and pick `Julia Monokai Vibrant` in the theme selector
(`ctrl-k ctrl-t`).

## Install as a dev extension

Zed command palette -> `zed: install dev extension` -> select this directory.

## Publish to the Zed extension registry

1. Push to GitHub (already done by setup).
2. Submit to [zed-industries/extensions](https://github.com/zed-industries/extensions)
   following
   [Developing Extensions](https://zed.dev/docs/extensions/developing-extensions).
3. Bump `version` in `extension.toml` for each release.

## Sources / attribution

- VS Code colors + Julia/Python token colors:
  `themes/julia-monokai-vibrant-color-theme.json` in
  CameronBieganek/julia-color-themes (MIT, (c) 2020 Cameron Bieganek).
- Upstream Monokai Vibrant by Dylan Marsh (MIT).
- Base Monokai from Microsoft VS Code (MIT).

## License

MIT. See `LICENSE`.
