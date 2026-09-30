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
mapping, not a copy. The mapping was verified token-by-token for a real Julia
file (`src/plotting.jl`) with a simulator that replays Zed's engine rules
against the installed `zed-julia` queries (`tree-sitter query` for captures,
last-pattern-wins for overlaps, longest dot-prefix key for resolution —
see `crates/language/src/buffer.rs::compute_chunk_highlights` and
`crates/syntax_theme/src/syntax_theme.rs::highlight_id`).
Re-run it with `python3 /tmp/opencode/sim.py`. Verified mappings for Julia:

- definitions purple `#AE81FF`, calls green `#81F900`, macros cyan `#00AAFF`
- `using`/`import`/`export`/`module` green `#81F900` (`keyword.import`)
- keywords red italic `#FF3F4F` (incl. `in`/`isa`/`where` via `keyword.operator`)
- strings yellow `#FFD945`, symbols `#FD5FF0`, `#` comments gray italic
- docstrings (`"""`) yellow upright via `comment.doc`, matching VS Code where
  docstrings are plain strings. Trade-off: `///` / `/** */` doc comments in
  other languages also render yellow instead of gray.
- `true`/`false`/`nothing`/`missing` blue `#00AAFF`, numbers blue `#00AAFF`
  (the Julia override group beats the generic pink `constant.numeric`)
- types cyan `#00AAFF`, defined struct names blue `#61afef`
- locals/`const` names white `#f8f8f0` (the grammar's later assignment rule
  correctly overrides `constant`), params orange italic `#FF9700`
- brackets orange `#FF8F3F` (author's `meta.bracket` rule), `,`/`;`/`.`/`$` white
- JSON keys teal `#56b6c2` (`property.json_key`), character literals pink,
  bare `escape` captures yellow, `obj.method()` calls green

Python files get best-effort styling through the same keys (booleans,
numbers, strings, `True`/`False`/`None`, decorators aside, all verified
against the source's Python section). Known Python deviations: plain and
method calls render purple via `function` (VS Code: green; definitions need
the purple), `import`/`from` render red italic (VS Code: green), `self`
renders red italic (VS Code: magenta), `def` params render white
(VS Code: light orange — upstream python queries capture no parameter).

Known structural deviations (grammar-determined, not fixable in a theme):

- `colorant"..."` prefixes render cyan (`function.macro` wins inside the
  prefixed-literal pattern); VS Code shows green.
- Constructor-like calls (`Theme(...)`) render green like all calls;
  VS Code shows them teal.
- `&&` / `||` / `!` render red (`operator`); VS Code shows them purple
  (`keyword.operator.boolean`) — one capture covers all operators.
- `'a'` character literals render yellow (`@string`); VS Code shows blue.
- Markdown block quotes and `---` separators have no Zed capture
  (render default white); VS Code shows them green / magenta.
- All brackets render orange here; VS Code only oranges `meta.bracket` scopes.
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
