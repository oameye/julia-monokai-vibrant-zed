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

## Color fidelity notes

VS Code uses TextMate scopes, Zed uses Tree-sitter captures, so a port is a
mapping, not a copy. The mapping was checked capture-by-capture against
`JuliaEditorSupport/zed-julia` (`languages/julia/highlights.scm`) and Zed's
resolution rule (a capture uses the longest dot-prefix key in `syntax`).
Verified mappings for Julia:

- definitions purple `#AE81FF`, calls green `#81F900`, macros cyan `#00AAFF`
- `using`/`import`/`export`/`module` green `#81F900` (`keyword.import`)
- keywords red italic `#FF3F4F` (incl. `in`/`isa`/`where` via `keyword.operator`)
- strings yellow `#FFD945`, symbols `#FD5FF0`, docstrings/comments gray italic
- `true`/`false`/`nothing`/`missing` blue `#00AAFF`, numbers pink `#E373CE`
- types cyan `#00AAFF`, defined struct names blue `#61afef`
- locals/params: white `#f8f8f0`, params orange italic `#FF9700`
- brackets orange `#FF8F3F` (author's `meta.bracket` rule), `,`/`;`/`.`/`$` white

Known structural deviations (cannot be 1:1):

- `const X = ...` names: white in VS Code (scoped as variables), cyan here if
  the `const_statement` query matches; currently renders white via the
  assignment rule.
- All brackets are orange here; VS Code only oranges `meta.bracket` scopes.
- Terminal ANSI colors are derived from the token palette; the VS Code source
  defines no terminal colors.
- `element.background` uses `#1d1f23` (input/dropdown bg); border uses
  `#181A1F` (source literally says `#181A11`, an apparent typo for `#1A1F`).
- Zed has no theme keys for selection color, scrollbar-active, titlebar text,
  or diff-insert background; closest available keys are mapped.

## Sources / attribution

- VS Code colors + Julia/Python token colors:
  `themes/julia-monokai-vibrant-color-theme.json` in
  CameronBieganek/julia-color-themes (MIT, (c) 2020 Cameron Bieganek).
- Upstream Monokai Vibrant by Dylan Marsh (MIT).
- Base Monokai from Microsoft VS Code (MIT).

## License

MIT. See `LICENSE`.
