Since https://github.com/helix-editor/helix/pull/2942 Helix can use external formatting programs available in the system `$PATH`.

- These settings should be added to `languages.toml` inside your config directory
- For each language `auto-format = true` and other settings are inherited from https://github.com/helix-editor/helix/blob/master/languages.toml
- They will override any formatting supplied by the language server


# Prettier https://prettier.io/

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

# shfmt https://github.com/patrickvane/shfmt

```
[[language]]
name = "bash"
formatter = { command = 'shfmt', args = ["-i", "4"] }
auto-format = true
```