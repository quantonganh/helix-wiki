Helix can use external formatting programs available in the system `$PATH`.

- Add these settings to `languages.toml` inside your config directory
- `auto-format = true` and other language settings are inherited from [languages.toml](https://github.com/helix-editor/helix/blob/master/languages.toml), there is no need to repeat them
- Specifying an external formatter will replace any formatting supplied by the language server
- Windows users [*may* need to specify the full path to the executable](https://github.com/helix-editor/helix/discussions/3198#discussioncomment-3325065)

# Prettier

https://prettier.io/

As of `v2.8.4` these languages are supported:

`flow|babel|babel-flow|babel-ts|typescript|acorn|espree|meriyah|css|less|scss|json|json5|json-stringify|graphql|markdown|mdx|vue|yaml|glimmer|html|angular|lwc`

The following have been tested: *Note: the args `--parser` is unlikely needed.*

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

[[language]]
name = "javascript"
formatter = { command = 'prettier', args = ["--parser", "typescript"] }
auto-format = true

[[language]]
name = "typescript"
formatter = { command = 'prettier', args = ["--parser", "typescript"] }
auto-format = true
```

```toml
[[language]]
name = "tsx"
formatter = { command = 'prettier', args = ["--parser", "typescript"] }
auto-format = true
```

Note: For **Windows** you may need to add `.cmd` to the command, example:

```
command = 'prettier.cmd'
```

# Deno

https://deno.land/

As of `v1.25.0` these languages are supported:

`ts, tsx, js, jsx, md, json, jsonc`

Deno's formatter is written in Rust and is *very* fast in comparison to Prettier. The formatting options are mostly copied from Prettier, but there are some differences.

- To see available formatting options: `deno fmt --help`
- `markdown` does not support formatting as many languages in fenced code blocks as Prettier

The following have been tested:

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
name = "jsx"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "jsx" ] }
auto-format = true

[[language]]
name = "tsx"
formatter = { command = 'deno', args = ["fmt", "-", "--ext", "tsx" ] }
auto-format = true
```

# shfmt

https://github.com/mvdan/sh#shfmt or https://github.com/patrickvane/shfmt

- `shfmt` formats shell programs
- To see available formatting options: `shfmt -h`

The following have been tested:

4 spaces:
```toml
[[language]]
name = "bash"
indent = { tab-width = 4, unit = "    " }
formatter = { command = 'shfmt', args = ["-i", "4"] }
auto-format = true
```

tabs:
```toml
[[language]]
name = "bash"
indent = { tab-width = 4, unit = "\t" }
formatter = { command = "shfmt" }
auto-format = true
```

# fish_indent

`fish_indent` is built into fish!

The following has been tested:

```toml
[[language]]
name = "fish"
formatter = { command = "fish_indent" }
auto-format = true
```

# Black

- `black` is an opinionated formatter for Python

```toml
[[language]]
name = "python"
formatter = { command = "black", args = ["--quiet", "-"] }
auto-format = true
```

# Rubocop

A Ruby static code analyzer and formatter, based on the community Ruby style guide.

```toml
[[language]]
name = "ruby"
formatter = { command = "bundle", args = ["exec", "rubocop", "--stdin", "foo.rb", "--fix", "--stderr", "--fail-level", "fatal"] }
auto-format = true
```

Weird arguments:
- `--stdin foo.rb`: Rubocop requires a filename for its reports, this is a dummy value to fulfill this. Call it whatever. Make it your own. Have fun with it.
- `--stderr`: Rubocop absolutely ALWAYS prints any errors it identifies. This sends them to stderr, otherwise they'd show up in your editor.
- `--fail-level`: Any error in the rubocop formatter will fail with errorcode 1. This can make you files not being able to save. raising the fail-evel to fatal will leave it on just for cases were rubocop is not working at all.


# StandardRB

A Ruby formatter that supports very little configuration so we can stop arguing about format and get on with our jobs. It's a wrapper around Rubocop so commands are basically identical.

```toml
[[language]]
name = "ruby"
formatter = { command = "bundle", args = ["exec", "standardrb", "--stdin", "foo.rb", "--fix", "--stderr"] }
auto-format = true
```

# SyntaxTree

Another formatting option for Ruby is [SyntaxTree](https://github.com/ruby-syntax-tree/syntax_tree), which is used "under the hood" by [Prettier for Ruby](https://github.com/prettier/plugin-ruby). It provides a few [configuration](https://github.com/ruby-syntax-tree/syntax_tree#configuration) options, either passed in as arguments or with a local `.streerc` file.

```toml
[[language]]
name = "ruby"
formatter = { command = "bundle", args = ["exec", "stree", "format"] }
auto-format = true
```

# gdformat

https://github.com/Scony/godot-gdscript-toolkit

A formatter for GDScript.

```toml
[[language]]
name = "gdscript"
formatter = { command = "gdformat", args = ["-"] }
auto-format = true
```