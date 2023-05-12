
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

## Astro


https://github.com/withastro/language-tools/tree/main/packages/language-server

```sh
npm install -g @astrojs/language-server
```

Sample settings in `languages.toml`

```toml
[[language]]
name = "astro"
scope = "source.astro"
injection-regex = "astro"
file-types = ["astro"]
roots = ["package.json", "astro.config.mjs"]
language-server = { command = "astro-ls", args = ["--stdio"] }
config = { "typescript" = { serverPath = "/home/user/path_to_my_project/node_modules/typescript/lib/tsserverlibrary.js" }, "environment" = "node" }
```

Please note that a valid absolute path to `tsserverlibrary.js` must be passed to the LSP config. The `config` key above could be omitted from the global config file and an additional config file in the workspace at `.helix/languages.toml` can be added to pass a different path for each project:

```toml
[[language]]
name = "astro"
config = { "typescript" = { serverPath = "/home/user/path_to_my_project/node_modules/typescript/lib/tsserverlibrary.js" }, "environment" = "node" }
```

## AWK

https://github.com/Beaglefoot/awk-language-server

```sh
npm install -g "awk-language-server@>=0.5.2"
```

## Bash

Language server for Bash, written using tree-sitter in TypeScript.

https://github.com/mads-hartmann/bash-language-server

`bash-language-server` can be installed via `NPM`:

```sh
npm i -g bash-language-server
```

## Bass

https://github.com/vito/bass/releases/latest

Bass's language server is built in to the `bass` command as `bass --lsp`. See the [Guide](https://bass-lang.org/guide.html#getting-started) for more info.

## BQN

bqnlsp: https://git.sr.ht/~detegr/bqnlsp, which depends on:

[cbqn-sys](https://github.com/Detegr/cbqn-sys) and 
[cbqn-rs](https://github.com/Detegr/cbqn-rs)

Sample settings in `languages.toml`

```toml
[[language]]
name = "bqn"
file-types = ["bqn"]
comment-token = "#"
indent = { tab-width = 2, unit = "  " }
shebangs = ["bqn", "cbqn"]
roots = []
injection-regex = "bqn"
scope = "scope.bqn"
language-server = { command = "bqnlsp", language-id = "bqn" }
```

Note: you can input the glyphs by [key remapping](https://docs.helix-editor.com/remapping.html) in `config.toml` like:

```toml
[keys.insert."\\"]
"=" = [ ":insert-output /bin/echo -n ×", "move_char_right" ]
minus = [ ":insert-output /bin/echo -n ÷", "move_char_right" ]
"+" = [ ":insert-output /bin/echo -n ⋆", "move_char_right" ]
# ...
```

## clangd

https://clangd.llvm.org/installation.html

**NOTE:** Clang >= 9 is recommended!

clangd relies on a [JSON compilation database](https://clang.llvm.org/docs/JSONCompilationDatabase.html) specified
as `compile_commands.json` or, for simpler projects, a `compile_flags.txt`.
For details on how to automatically generate one using CMake look [here](https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html). Alternatively, you can use [Bear](https://github.com/rizsotto/Bear).

## CSS

https://github.com/hrsh7th/vscode-langservers-extracted

`css-languageserver` can be installed via `npm`:

```sh
npm i -g vscode-langservers-extracted
```

## OmniSharp

https://github.com/omnisharp/omnisharp-roslyn
OmniSharp server based on Roslyn workspaces

`omnisharp-roslyn` can be installed by downloading and extracting a release for your platform from [here](https://github.com/OmniSharp/omnisharp-roslyn/releases).
Omnisharp can also be built from source by following the instructions [here](https://github.com/omnisharp/omnisharp-roslyn#downloading-omnisharp). 

Omnisharp requires the [dotnet-sdk](https://dotnet.microsoft.com/download) to be installed.

### Usage

#### Windows

To use Omnisharp, you only need to have the `OmniSharp` binary in your environment path. The default `languages.toml` configuration should work fine:

```
[[language]]
name = "c-sharp"
language-server.command = "OmniSharp"
```

#### macOS

Because OmniSharp is not shipped as a binary file, instead as `OmniSharp.dll`, it needs to be run using `dotnet`. As such the `languages.toml` config should be changed to this:

```
[[language]]
name = "c-sharp"
language-server = { command = "dotnet", args = [ "path/to/OmniSharp.dll", "--languageserver" ] }
```

## CMake

CMake LSP Implementation.

https://github.com/regen100/cmake-language-server

## D

Serve-D.

https://github.com/Pure-D/serve-d

Install using ```dub fetch serve-d```

## Dart

Language server for dart.

https://github.com/dart-lang/sdk/tree/master/pkg/analysis_server/tool/lsp_spec

## Deno

Install Deno from https://deno.land/#installation

Deno requires custom configuration in `languages.toml` see https://github.com/denoland/deno/issues/14455

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

Note that some lsp commands are not currently supported, in particular `go_to_definition` because it requires a Deno lsp extension https://deno.land/manual/language_server/overview.

## Docker

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

## Elixir

https://github.com/elixir-lsp/elixir-ls

`elixir-ls` can be installed by following the instructions [here](https://github.com/elixir-lsp/elixir-ls#building-and-running).

```bash
curl -fLO https://github.com/elixir-lsp/elixir-ls/releases/latest/download/elixir-ls.zip
unzip elixir-ls.zip -d /path/to/elixir-ls
# Unix
chmod +x /path/to/elixir-ls/language_server.sh
```

You also need to rename `language_server.sh` to `elixir-ls` and add it to your `$PATH`, because that's how `helix` expects to find it.

## Elm

https://github.com/elm-tooling/elm-language-server#installation

```sh
npm install -g elm elm-test elm-format @elm-tooling/elm-language-server
```

## Unison

Unison language server.

More info: https://github.com/unisonweb/unison/blob/trunk/docs/language-server.markdown

Requirements:
- `ucm` started
- `ncat`, `nc` or `netcat`

To `~/.config/helix/languages.toml` append this code:

```toml
[[language]]
name = "unison"
scope = "source.unison"
injection-regex = "unison"
file-types = ["u"]
shebangs = []
roots = []
auto-format = false
comment-token = "--"
indent = { tab-width = 4, unit = "    " }
language-server = { command = "ncat", args = ["localhost", "5757"] }
```

## GDScript

We need to install `nc` or `netcat`. Port 6005 is used in Godot 4.0 beta6. You will find the right value in the editor configuration panel.

```toml
[[language]]
name = "gdscript"
roots = ["project.godot"]
language-server = { command = "nc", args = ["localhost", "6005"], language-id = "gdscript" }
```

**For Windows 10/11**

Use `winget` to install `nmap`. This will install `ncat`.

```powershell
winget install nmap
```
Once installed, make sure the folder that `nmap` is now located at is added to your PATH, as `winget` fails to do this automatically for some people.

In Godot 3.5.1 port used is `6008`. You have to change the command used also. Instead of `nc` type `ncat` and modify the port. You can find the port when you open the Godot editor and navigate here: `Editor -> Editor Settings -> Network -> Language Server -> Remote Port`.

```toml
[[language]]
name = "gdscript"
roots = ["project.godot"]
language-server = { command = "ncat", args = ["localhost", "6008"], language-id = "gdscript" }
```

## Gleam

Starting with version `0.21.0`, the Gleam language server is built-in to the `gleam` command-line interface. [See the official announcement for more information.](https://gleam.run/news/v0.21-introducing-the-gleam-language-server/)

```sh
gleam lsp
```

## Go

Google's LSP server for golang.

https://github.com/golang/tools/tree/master/gopls

The folder for go packages (typically $HOME/go/bin) will need to be added to your PATH as well

## HTML

https://github.com/hrsh7th/vscode-langservers-extracted

`vscode-html-language-server` can be installed via `npm`:

```sh
npm i -g vscode-langservers-extracted
```

## Haskell

Haskell Language Server.

https://github.com/haskell/haskell-language-server

## PHP

https://intelephense.com/

`intelephense` can be installed via `npm`:

```sh
npm install -g intelephense
```

## JavaScript

See [tsserver](https://github.com/helix-editor/helix/wiki/How-to-install-the-default-language-servers#typescript).

## JSON

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

## Jsonnet

https://github.com/grafana/jsonnet-language-server

A [Language Server Protocol (LSP)](https://langserver.org/) server for [Jsonnet](https://jsonnet.org/).

Can be installed either via the [latest release binary](https://github.com/grafana/jsonnet-language-server/releases)
or if you have golang installed, you can use:

```sh
go install github.com/grafana/jsonnet-language-server@latest
```

## TypeScript

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
## Java

https://github.com/eclipse/eclipse.jdt.ls

Installation instructions can be found on the [projects README](https://github.com/eclipse/eclipse.jdt.ls).

On macOS installation can also be done via `brew install jdtls`.

For `jdtls` versions older than `1.16.0`: the `-data` parameter must be passed to `jdtls` and it must be different for each project. This can be achieved by adding a `.helix/languages.toml` configuration to the project root:

```toml
[[language]]
name = "java"
language-server = { command = "jdtls", args = ["-data", "/home/my_user/.cache/jdtls/my_project"] }
```

Note: the `-data` parameter must be outside the project directory.

## Julia

https://github.com/julia-vscode/LanguageServer.jl

LanguageServer.jl can be installed with `julia` and `Pkg`:

```sh
julia -e 'using Pkg; Pkg.add("LanguageServer")'
```

To update an existing install, use the following command:

```sh
julia -e 'using Pkg; Pkg.update()'
```

## Kotlin

A Kotlin language server which was developed for internal usage and
released afterward. Maintaining is not done by the original author,
but by fwcd.

It is built via gradle and developed on GitHub.
Source and additional description:
https://github.com/fwcd/kotlin-language-server

## Lean 3

https://github.com/leanprover/lean-client-js/tree/master/lean-language-server

Lean installation instructions can be found
[here](https://leanprover-community.github.io/get_started.html#regular-install).

Once Lean is installed, you can install the Lean 3 language server by running

```sh
npm install -g lean-language-server
```

## Lua 

https://github.com/sumneko/lua-language-server/wiki/Precompiled-Binaries

`mac`
```sh
brew install lua-language-server
```

## Markdown

### Marksman

The default language server is Marksman: https://github.com/artempyanykh/marksman

Binaries are available from: https://github.com/artempyanykh/marksman/releases

`macOS and Linux`
```sh
brew install marksman or yay -S marksman-bin
```

`Windows`
```pwsh
scoop install marksman
```

### ltex-ls

As an alternative you can use `ltex-ls` which provides grammar and spelling errors in markup documents: https://valentjn.github.io/ltex/ltex-ls/installation.html

```toml
[[language]]
name = "markdown"
language-server = { command = "ltex-ls" }
```

Additional configuration settings can be added, for example to disable the profanity rules and add the word `builtin` to two dictionaries:

```toml
config = { ltex.disabledRules = { "en-US" = [
  "PROFANITY",
], "en-GB" = [
  "PROFANITY",
] }, ltex.dictionary = { "en-US" = [
  "builtin",
], "en-GB" = [
  "builtin",
] } }
```

Currently, [the ability to add to your user dictionary while running Helix is not supported](https://github.com/valentjn/ltex-ls/issues/231), so adding words to the config is the best workaround.


## Scala

Scala language server with rich IDE features. 

https://scalameta.org/metals/

1. Install [Coursier](https://get-coursier.io/)
2. Run `coursier install metals`

## Markdoc

[markdoc-ls](https://github.com/markdoc-extra/markdoc-ls) - an experimental language server for markdoc.

Install using

```sh
npm install -g markdoc-ls
```

## Mint

https://www.mint-lang.com

Install Mint using the [instructions](https://www.mint-lang.com/install).
The language server is included since version 0.12.0.

## Nim

https://github.com/nim-lang/langserver

```sh
# May require choosenim
nimble install nimlangserver
```

## OCaml

https://github.com/ocaml/ocaml-lsp

The OCaml language server `ocamllsp` can be installed via OPAM:

```sh
opam install ocaml-lsp-server
```

## Perl

https://github.com/bscan/PerlNavigator

Provides syntax checking, autocompletion, perlcritic, code navigation, hover for Perl.

Implemented as a Language Server using the Microsoft LSP libraries along with Perl doing the syntax checking and parsing.

Perl Navigator can be installed by downloading the latest release for your platform at [the project's releases page](https://github.com/bscan/PerlNavigator/releases) and putting the perlnavigator executable somewhere in your PATH.


## Prisma

https://github.com/prisma/language-tools/tree/main/packages/language-server

`prisma-language-server` can be installed via npm:

```sh
npm install -g @prisma/language-server
```

## Python - pylsp

[python-lsp/python-lsp-server](https://github.com/python-lsp/python-lsp-server) (`pylsp`) is a fork of the python-language-server project (`pyls`), maintained by the Spyder IDE team and the community.
It is a Python 3.7+ implementation of the [Language Server Protocol](https://github.com/Microsoft/language-server-protocol) (versions <1.4 should still work with Python 3.6).

Installation instructions can be found in the [project's README](https://github.com/python-lsp/python-lsp-server#installation), but it consists of installing a package using `pip` (or [`pipx`](https://github.com/pypa/pipx)):

```console
pip install -U 'python-lsp-server[all]'
```

The `[all]` above refers to the optional providers supported.
You can fine-tune what to install following the instructions [here](https://github.com/python-lsp/python-lsp-server#installation).

### python-lsp-ruff

[python-lsp/python-lsp-ruff](https://github.com/python-lsp/python-lsp-ruff) is a plugin for pylsp that provides support for [ruff (see below)](#ruff).
See [installation instructions](https://github.com/python-lsp/python-lsp-ruff#install).

The plugin supports [some configuration](https://github.com/python-lsp/python-lsp-ruff#configuration), but it should work out of the box after installing.

## Python - pyright

Pyright is a fast type checker and language server from Microsoft, meant for large Python source bases. It is the LSP part of pylance (the VS Code python daemon).

https://github.com/microsoft/pyright

The language server can be installed by running `npm install --location=global pyright`

It has odd handling of client configuration so the following addition to `languages.toml` is required:

```toml
[[language]]
name = "python"
roots = ["pyproject.toml"]
language-server = { command = "pyright-langserver", args = ["--stdio"] }
config = {} # <- this is the important line
```

## Python - ruff

[charliermarsh/ruff](https://github.com/charliermarsh/ruff) is an extremely fast Python linter, written in Rust (see [installation instructions](https://github.com/charliermarsh/ruff#installation-and-usage)).

An LSP for it is available through [charliermarsh/ruff-lsp](https://github.com/charliermarsh/ruff-lsp) (see [installation instructions](https://github.com/charliermarsh/ruff-lsp#installation-and-usage)).

A suggested Helix configuration using ruff-lsp is given below (based on [charliermarsh/ruff-lsp#example-helix](https://github.com/charliermarsh/ruff-lsp#example-helix)):

```toml
[[language]]
name = "python"
language-server = { command = "ruff-lsp" }

# In case you'd like to use ruff alongside black for code formatting:
formatter = { command = "black", args = ["--quiet", "-"] }
auto-format = true
```

**Note** that ruff lacks basic features and is meant to be used alongside another LSP ([helix-editor/helix#5399 (comment)](https://github.com/helix-editor/helix/issues/5399#issuecomment-1373470899), [charliermarsh/ruff-lsp#23](https://github.com/charliermarsh/ruff-lsp/issues/23), [charliermarsh/ruff-lsp#23 (comment)](https://github.com/charliermarsh/ruff-lsp/issues/23#issuecomment-1367903296)).

As an alternative, [pylsp](#pylsp) has support for ruff via a plugin.
[See instructions for Helix here](#python-lsp-ruff)

## OpenPolicyAgent

An implementation of the language server protocol for OpenPolicyAgent's rego.

You can download it from its [releases page](https://github.com/kitagry/regols/releases), or

```sh
$ go install github.com/kitagry/regols@latest
```

## R

An implementation of the Language Server Protocol for R.

https://github.com/REditorSupport/languageserver

The language server can be installed by running `R -e 'install.packages("languageserver")'`.

## Racket

[https://github.com/jeapostrophe/racket-langserver](https://github.com/jeapostrophe/racket-langserver)

The Racket language server. This project seeks to use
[DrRacket](https://github.com/racket/drracket)'s public API to provide
functionality that mimics DrRacket's code tools as closely as possible.

Install via `raco`: `raco pkg install racket-langserver`

## ReScript

https://github.com/rescript-lang/rescript-vscode

// ReScript language server.

## Nix

A language server for Nix providing basic completion and formatting via nixpkgs-fmt.

https://github.com/nix-community/rnix-lsp

To install manually, run `cargo install rnix-lsp`. If you are using nix, rnix-lsp is in nixpkgs.

This server accepts configuration via the `settings` key.

## Rust

rust-analyzer (aka rls 2.0), a language server for Rust.

https://github.com/rust-analyzer/rust-analyzer

You can install rust-analyzer using `rustup` starting from Rust 1.64, and it will be added to your system's `$PATH` [starting from Rustup 1.26.0](https://blog.rust-lang.org/2023/04/25/Rustup-1.26.0.html#whats-new-in-rustup-1260):

```sh
rustup component add rust-analyzer
```

Add the following to your `languages.toml` to enable [clippy](<https://github.com/rust-lang/rust-clippy>) on save:

```toml
[[language]]
name = "rust"

[language.config.check]
command = "clippy"
```

See [docs](https://rust-analyzer.github.io/manual.html) for extra settings. Everything under the rust-analyzer key goes under language.config key in helix (for example, `rust-analyzer.check.command = "clippy"` is translated into the `language.toml` as above.)

## SCSS

SCSS's language server is available from the vscode-langservers-extracted collection:

https://github.com/hrsh7th/vscode-langservers-extracted

You may install it by running:

```sh
npm i -g vscode-langservers-extracted
```

## Slint

<https://github.com/slint-ui/slint/tree/HEAD/tools/lsp>  
<https://slint-ui.com/>

```sh
cargo install slint-lsp
```

## Smithy

For Smithy projects the following LSP is used:
https://github.com/awslabs/smithy-language-server

[coursier](https://get-coursier.io/) must be installed so that the language server can be launched. To install coursier please see their [installation instructions](https://get-coursier.io/docs/cli-installation#native-launcher).
Since coursier will take care of everything else, no other steps are necessary!


## Swift

A language server for Swift, formatting provided via swift-format

https://github.com/apple/sourcekit-lsp

https://github.com/apple/swift-format

Follow the [Getting Started](https://github.com/apple/sourcekit-lsp#getting-started) guide to get sourcekit-lsp installed correctly for your OS.
No additional configuration is needed, though note to use the same toolchain for both your installed LSP, and that you use to build.


## Solargraph

https://solargraph.org/

Solargraph, a language server for Ruby

You can install Solargraph via gem install.

```sh
gem install --user-install solargraph
```

## solc

solc is the native language server for the Solidity language.

https://docs.soliditylang.org/en/latest/installing-solidity.html

## Svelte

https://github.com/sveltejs/language-tools/tree/master/packages/language-server

`svelte-language-server` can be installed via `npm`:

```sh
npm install -g svelte-language-server
```

## TOML

https://taplo.tamasfe.dev/

The `full` version (with the language server) can be downloaded from:

`binaries`: [taplo releases](https://github.com/tamasfe/taplo/releases)

`cargo`:
```sh
cargo install taplo-cli --locked --features lsp
```
** The NPM versions of taplo does not contain the language server at this time

Run `taplo lsp --help` for more info.

## WGSL

https://github.com/wgsl-analyzer/wgsl-analyzer

`wgsl_analyzer` can be installed via `cargo`:
```sh
cargo install --git https://github.com/wgsl-analyzer/wgsl-analyzer wgsl_analyzer
```

## Vue

https://github.com/vuejs/vetur/tree/master/server

The Vue language server `vls` can be installed via NPM:

```sh
npm install -g vls
```

## YAML

https://github.com/redhat-developer/yaml-language-server

`yaml-language-server` can be installed via `brew` on Mac:

```sh
brew install yaml-language-server
```

Example on configuring the language server with a schema.
```toml
[[language]]
name = "yaml"

[language.config.yaml]
format = { enable = true }
validation = true

[language.config.yaml.schemas]
"https://json.schemastore.org/github-workflow.json" = ".github/workflows/*.{yml,yaml}"
```

## Zig

Zig LSP implementation + Zig Language Server.

https://github.com/zigtools/zls
