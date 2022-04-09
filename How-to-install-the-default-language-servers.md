To show the list of default language servers for your version of Helix please use `hx --health`.

For Helix to use these language servers they must first be installed onto your computer. Once installed they will be used automatically with no further setup needed.

Check if your operating system repository has them available, or install them manually following the instructions below.

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

## omnisharp

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

## dockerls

https://github.com/rcjsuen/dockerfile-language-server-nodejs

`docker-langserver` can be installed via `npm`:

```sh
npm install -g dockerfile-language-server-nodejs
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

## julials

https://github.com/julia-vscode/julia-vscode

LanguageServer.jl can be installed with `julia` and `Pkg`:

```sh
julia --project=~/.julia/environments/nvim-lspconfig -e 'using Pkg; Pkg.add("LanguageServer")'
```

where `~/.julia/environments/nvim-lspconfig` is the location where
the default configuration expects LanguageServer.jl to be installed.

To update an existing install, use the following command:

```sh
julia --project=~/.julia/environments/nvim-lspconfig -e 'using Pkg; Pkg.update()'
```

Note: In order to have LanguageServer.jl pick up installed packages or dependencies in a
Julia project, you must make sure that the project is instantiated:

```sh
julia --project=/path/to/my/project -e 'using Pkg; Pkg.instantiate()'
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

## mint

https://www.mint-lang.com

Install Mint using the [instructions](https://www.mint-lang.com/install).
The language server is included since version 0.12.0.

## R languageserver

An implementation of the Language Server Protocol for R.

https://github.com/REditorSupport/languageserver

The language server can be installed by running `R -e 'install.packages("languageserver")'`.

## rnix

A language server for Nix providing basic completion and formatting via nixpkgs-fmt.

https://github.com/nix-community/rnix-lsp

To install manually, run `cargo install rnix-lsp`. If you are using nix, rnix-lsp is in nixpkgs.

This server accepts configuration via the `settings` key.

## sourcekit-lsp and swift-format

A language server for Swift, formatting provided via swift-format

https://github.com/apple/sourcekit-lsp

https://github.com/apple/swift-format

Follow the [Getting Started](https://github.com/apple/sourcekit-lsp#getting-started) guide to get sourcekit-lsp installed correctly for your OS.
No additional configuration is needed, though note to use the same toolchain for both your installed LSP, and that you use to build.

## pylsp

A Python 3.6+ implementation of the Language Server Protocol.

https://github.com/python-lsp/python-lsp-server

The language server can be installed via `pipx install 'python-lsp-server[all]'`.
Further instructions can be found in the [project's README](https://github.com/python-lsp/python-lsp-server).

Note: This is a community fork of `pyls`.

## racket_langserver

[https://github.com/jeapostrophe/racket-langserver](https://github.com/jeapostrophe/racket-langserver)

The Racket language server. This project seeks to use
[DrRacket](https://github.com/racket/drracket)'s public API to provide
functionality that mimics DrRacket's code tools as closely as possible.

Install via `raco`: `raco pkg install racket-langserver`

## rescriptls

https://github.com/rescript-lang/rescript-vscode

ReScript language server

## solargraph

https://solargraph.org/

solargraph, a language server for Ruby

You can install solargraph via gem install.

```sh
gem install --user-install solargraph
```

## rust_analyzer

https://github.com/rust-analyzer/rust-analyzer

rust-analyzer (aka rls 2.0), a language server for Rust

See [docs](https://github.com/rust-analyzer/rust-analyzer/tree/master/docs/user#settings) for extra settings.

## metals

Scala language server with rich IDE features.

https://scalameta.org/metals/

See full instructions in the Metals documentation:

https://scalameta.org/metals/docs/editors/vim.html#using-an-alternative-lsp-client

## solc

solc is the native language server for the Solidity language.

https://docs.soliditylang.org/en/latest/installing-solidity.html

## svelte

https://github.com/sveltejs/language-tools/tree/master/packages/language-server

`svelte-language-server` can be installed via `npm`:

```sh
npm install -g svelte-language-server
```

## zls

Zig LSP implementation + Zig Language Server.

https://github.com/zigtools/zls

## ocamllsp

https://github.com/ocaml/ocaml-lsp

The OCaml language server `ocamllsp` can be installed via OPAM:

```sh
opam install ocaml-lsp-server
```
## vls

https://github.com/vuejs/vetur/tree/master/server

The Vue language server `vls` can be installed via npm:

```sh
npm install -g vls
```