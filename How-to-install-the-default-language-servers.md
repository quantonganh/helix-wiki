To show the list of default language servers for your version of Helix please use `hx --health`.

For Helix to use these language servers they must first be installed onto your computer. Once installed they will be used automatically with no further setup needed.

Check if your operating system repository has them available, or install them manually following the instructions below.

If your language server does not support stdio, you can use `netcat` as a drop-in proxy, just add this to your `languages.toml`:
```toml
[[language]]
name = "example"
language-server = { command = "nc", args = ["localhost", "6008"] }
```
Much of this information was originally sourced from [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md), thanks to those authors!

## bashls

Language server for bash, written using tree sitter in typescript.

https://github.com/mads-hartmann/bash-language-server

`bash-language-server` can be installed via `npm`:

```sh
npm i -g bash-language-server
```

## clangd

https://clangd.llvm.org/installation.html

**NOTE:** Clang >= 9 is recommended!

clangd relies on a [JSON compilation database](https://clang.llvm.org/docs/JSONCompilationDatabase.html) specified
as compile_commands.json or, for simpler projects, a compile_flags.txt.
For details on how to automatically generate one using CMake look [here](https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html). Alternatively, you can use [Bear](https://github.com/rizsotto/Bear).

## cssls

https://github.com/hrsh7th/vscode-langservers-extracted

`css-languageserver` can be installed via `npm`:

```sh
npm i -g vscode-langservers-extracted
```

## OmniSharp

https://github.com/omnisharp/omnisharp-roslyn
OmniSharp server based on Roslyn workspaces

`omnisharp-roslyn` can be installed by downloading and extracting a release from [here](https://github.com/OmniSharp/omnisharp-roslyn/releases).
Omnisharp can also be built from source by following the instructions [here](https://github.com/omnisharp/omnisharp-roslyn#downloading-omnisharp).

Omnisharp requires the [dotnet-sdk](https://dotnet.microsoft.com/download) to be installed.

## cmake

CMake LSP Implementation.

https://github.com/regen100/cmake-language-server

## dartls

Language server for dart.

https://github.com/dart-lang/sdk/tree/master/pkg/analysis_server/tool/lsp_spec

## deno

Install deno from https://deno.land/#installation

deno requires custom configuration in languages.toml see https://github.com/denoland/deno/issues/14455

```toml
[[language]]
name = "javascript"
shebangs = ["deno", "node"]
roots = ["deno.json", "package.json", "tsconfig.json"]
config = { enable = true, lint = true, unstable = true }
language-server = { command = "deno", args = ["lsp"], language-id = "javascript" }

[[language]]
name = "jsx"
shebangs = ["deno", "node"]
roots = ["deno.json", "package.json", "tsconfig.json"]
config = { enable = true, lint = true, unstable = true }
language-server = { command = "deno", args = ["lsp"], language-id = "javascriptreact" }

[[language]]
name = "typescript"
shebangs = ["deno", "node"]
roots = ["deno.json", "package.json", "tsconfig.json"]
config = { enable = true, lint = true, unstable = true }
language-server = { command = "deno", args = ["lsp"], language-id = "typescript" }

[[language]]
name = "tsx"
shebangs = ["deno", "node"]
roots = ["deno.json", "package.json", "tsconfig.json"]
config = { enable = true, lint = true, unstable = true }
language-server = { command = "deno", args = ["lsp"], language-id = "typescriptreact" }
```

Note that some lsp commands are not currently supported, in particular `go_to_definition` because it requires a deno lsp extension https://deno.land/manual/language_server/overview.

## dockerls

https://github.com/rcjsuen/dockerfile-language-server-nodejs

`docker-langserver` can be installed via `npm`:

```sh
npm install -g dockerfile-language-server-nodejs
```

## dot Graphviz

https://github.com/nikeee/dot-language-server

```sh
npm i -g dot-language-server
```

## elixir-ls

https://github.com/elixir-lsp/elixir-ls

`elixir-ls` can be installed by following the instructions [here](https://github.com/elixir-lsp/elixir-ls#building-and-running).

```bash
curl -fLO https://github.com/elixir-lsp/elixir-ls/releases/latest/download/elixir-ls.zip
unzip elixir-ls.zip -d /path/to/elixir-ls
# Unix
chmod +x /path/to/elixir-ls/language_server.sh
```

You also need to rename `language_server.sh` to `elixir-ls` and add it to your `$PATH`, because that's how `helix` expects to find it.

## elmls

https://github.com/elm-tooling/elm-language-server#installation

```sh
npm install -g elm elm-test elm-format @elm-tooling/elm-language-server
```

## gopls

Google's lsp server for golang.

https://github.com/golang/tools/tree/master/gopls

## html

https://github.com/hrsh7th/vscode-langservers-extracted

`vscode-html-language-server` can be installed via `npm`:

```sh
npm i -g vscode-langservers-extracted
```

## hls

Haskell Language Server.

https://github.com/haskell/haskell-language-server

## intelephense

https://intelephense.com/

`intelephense` can be installed via `npm`:

```sh
npm install -g intelephense
```

## jsonls

https://github.com/hrsh7th/vscode-langservers-extracted

vscode-json-language-server, a language server for JSON and JSON schema

`vscode-json-language-server` can be installed via `npm`:
```sh
npm i -g vscode-langservers-extracted
```

Available settings can be found here: https://github.com/microsoft/vscode/blob/4f69cdf95a12cef48d405b38bf7812a7f297c310/extensions/json-language-features/server/src/jsonServer.ts#L183

Usage
```toml
config = { "provideFormatter" = true, "json" = { "keepLines" = { "enable" = true } } }
```

## jsonnet

https://github.com/grafana/jsonnet-language-server

A [Language Server Protocol (LSP)](https://langserver.org/) server for [Jsonnet](https://jsonnet.org/).

Can be installed either via the [latest release binary](https://github.com/grafana/jsonnet-language-server/releases)
or if you have golang installed, you can use:

```sh
go install github.com/grafana/jsonnet-language-server@latest
```

## tsserver

https://github.com/theia-ide/typescript-language-server

`typescript-language-server` depends on `typescript`. Both packages can be installed via `npm`:

```sh
npm install -g typescript typescript-language-server
```

To configure type language server, add a
[`tsconfig.json`](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) or
[`jsconfig.json`](https://code.visualstudio.com/docs/languages/jsconfig) to the root of your
project.

Here's an example that disables type checking in JavaScript files.

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es6",
    "checkJs": false
  },
  "exclude": ["node_modules"]
}
```
## Java Eclipse JDT Language Server

https://github.com/eclipse/eclipse.jdt.ls

Installation instructions can be found on the [projects README](https://github.com/eclipse/eclipse.jdt.ls).

On MacOS installation can also be done via `brew install jdtls`.

The `-data` parameter must be passed to `jdtls` and it must be different for each project. This can be achieved by adding a `.helix/languages.toml` configuration to the projects root:

```toml
[[language]]
name = "java"
language-server = { command = "jdtls", args = ["-data", "/home/my_user/.cache/jdtls/data/my_project"] }
```

## julials

https://github.com/julia-vscode/LanguageServer.jl

LanguageServer.jl can be installed with `julia` and `Pkg`:

```sh
julia -e 'using Pkg; Pkg.add("LanguageServer")'
```

To update an existing install, use the following command:

```sh
julia -e 'using Pkg; Pkg.update()'
```

## kotlin_language_server

A kotlin language server which was developed for internal usage and
released afterwards. Maintaining is not done by the original author,
but by fwcd.

It is built via gradle and developed on github.
Source and additional description:
https://github.com/fwcd/kotlin-language-server

## lean3ls

https://github.com/leanprover/lean-client-js/tree/master/lean-language-server

Lean installation instructions can be found
[here](https://leanprover-community.github.io/get_started.html#regular-install).

Once Lean is installed, you can install the Lean 3 language server by running

```sh
npm install -g lean-language-server
```

## lua 

https://github.com/sumneko/lua-language-server/wiki/Precompiled-Binaries

`mac`
```sh
brew install lua-language-server
```

## markdown
ltex-ls provides grammar and spelling errors in markup documents

https://valentjn.github.io/ltex/ltex-ls/installation.html

```toml
[[language]]
name = "markdown"
language-server = { command = "ltex-ls" }
file-types = ["md"]
scope = "source.markdown"
roots = []
```

## metals

Scala language server with rich IDE features.

https://scalameta.org/metals/

See full instructions in the Metals documentation:

https://scalameta.org/metals/docs/editors/vim.html#using-an-alternative-lsp-client

## mint

https://www.mint-lang.com

Install Mint using the [instructions](https://www.mint-lang.com/install).
The language server is included since version 0.12.0.

## nimlsp

https://github.com/PMunch/nimlsp

```sh
nimble install nimlsp
```

## ocamllsp

https://github.com/ocaml/ocaml-lsp

The OCaml language server `ocamllsp` can be installed via OPAM:

```sh
opam install ocaml-lsp-server
```

## prisma

https://github.com/prisma/language-tools/tree/main/packages/language-server

`prisma-language-server` can be installed via npm:

```sh
npm install -g @prisma/language-server
```

## pylsp

A Python 3.6+ implementation of the Language Server Protocol.

https://github.com/python-lsp/python-lsp-server

The language server can be installed via `pipx install 'python-lsp-server[all]'`.
Further instructions can be found in the [project's README](https://github.com/python-lsp/python-lsp-server).

Note: This is a community fork of `pyls`.

## R languageserver

An implementation of the Language Server Protocol for R.

https://github.com/REditorSupport/languageserver

The language server can be installed by running `R -e 'install.packages("languageserver")'`.

## racket_langserver

[https://github.com/jeapostrophe/racket-langserver](https://github.com/jeapostrophe/racket-langserver)

The Racket language server. This project seeks to use
[DrRacket](https://github.com/racket/drracket)'s public API to provide
functionality that mimics DrRacket's code tools as closely as possible.

Install via `raco`: `raco pkg install racket-langserver`

## rescriptls

https://github.com/rescript-lang/rescript-vscode

ReScript language server

## rnix

A language server for Nix providing basic completion and formatting via nixpkgs-fmt.

https://github.com/nix-community/rnix-lsp

To install manually, run `cargo install rnix-lsp`. If you are using nix, rnix-lsp is in nixpkgs.

This server accepts configuration via the `settings` key.

## rust_analyzer

https://github.com/rust-analyzer/rust-analyzer

rust-analyzer (aka rls 2.0), a language server for Rust

See [docs](https://github.com/rust-analyzer/rust-analyzer/tree/master/docs/user#settings) for extra settings.

## slint-lsp

<https://github.com/slint-ui/slint/tree/HEAD/tools/lsp>  
<https://slint-ui.com/>

```sh
cargo install slint-lsp
```

## sourcekit-lsp and swift-format

A language server for Swift, formatting provided via swift-format

https://github.com/apple/sourcekit-lsp

https://github.com/apple/swift-format

Follow the [Getting Started](https://github.com/apple/sourcekit-lsp#getting-started) guide to get sourcekit-lsp installed correctly for your OS.
No additional configuration is needed, though note to use the same toolchain for both your installed LSP, and that you use to build.


## solargraph

https://solargraph.org/

solargraph, a language server for Ruby

You can install solargraph via gem install.

```sh
gem install --user-install solargraph
```

## solc

solc is the native language server for the Solidity language.

https://docs.soliditylang.org/en/latest/installing-solidity.html

## svelte

https://github.com/sveltejs/language-tools/tree/master/packages/language-server

`svelte-language-server` can be installed via `npm`:

```sh
npm install -g svelte-language-server
```

## toml

https://taplo.tamasfe.dev/

The `full` version (with the language server) can be downloaded from:

`binaries`: [taplo releases](https://github.com/tamasfe/taplo/releases)

`cargo`:
```sh
cargo install taplo-cli --locked --features lsp
```
** The NPM versions of taplo do not contain the language server at this time

Run `taplo lsp --help` for more info.

## wgsl_analyzer

https://github.com/wgsl-analyzer/wgsl-analyzer

`wgsl_analyzer` can be installed via `cargo`:
```sh
cargo install --git https://github.com/wgsl-analyzer/wgsl-analyzer wgsl_analyzer
```

## vls

https://github.com/vuejs/vetur/tree/master/server

The Vue language server `vls` can be installed via npm:

```sh
npm install -g vls
```

## zls

Zig LSP implementation + Zig Language Server.

https://github.com/zigtools/zls
