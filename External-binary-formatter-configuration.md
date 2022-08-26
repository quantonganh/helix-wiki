Since https://github.com/helix-editor/helix/pull/2942 Helix can use external formatting programs available in the system `$PATH`.

- Add these settings to `languages.toml` inside your config directory
- `auto-format = true` and other language settings are inherited from https://github.com/helix-editor/helix/blob/master/languages.toml, there is no need to repeat them
- Specifying an external formatter will replace any formatting supplied by the language server


# Prettier

https://prettier.io/

* Windows users may need to specify the full path to the `prettier` executable: https://github.com/helix-editor/helix/discussions/3198#discussioncomment-3325065

```toml
[[language]]
name = "html"
formatter = { command = 'prettier', args = ["--parser", "html"] }

[[language]]
name = "json"
formatter = { command = 'prettier', args = ["--parser", "json"] }

[[language]]
name = "css"
formatter = { command = 'prettier', args = ["--parser", "css"] }
auto-format = true

[[language]]
name = "javascript"
formatter = { command = 'prettier', args = ["--parser", "typescript"] }
auto-format = true

[[language]]
name = "typescript"
formatter = { command = 'prettier', args = ["--parser", "typescript"] }
auto-format = true
```

# shfmt

https://github.com/patrickvane/shfmt

```toml
[[language]]
name = "bash"
formatter = { command = 'shfmt', args = ["-i", "4"] }
auto-format = true
```

# Deno

https://deno.land/

Deno's formatter is written in Rust and is *very* fast in comparison to Prettier. The formatting options are mostly copied from Prettier, but there are some differences.

- To see available formatting options: `deno fmt --help`
- `jsonc` and `jsx` are supported by Deno, but not currently supported by Helix

```toml
[[language]]
name = "javascript"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "js" ] }
auto-format = true

[[language]]
name = "json"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "json" ] }

[[language]]
name = "markdown"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "md" ] }
auto-format = true

[[language]]
name = "typescript"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "ts" ] }
auto-format = true

[[language]]
name = "tsx"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "tsx" ] }
auto-format = true
```