* [Missing syntax highlighting](#missing-syntax-highlighting)
* [LSP isn't working](#lsp-isn-t-working)

### Missing syntax highlighting

Did you copy the `runtime` folder along with the `languages.toml` configuration file? By default, Helix will look for the runtime inside the same folder as the executable, but that can be overridden via the `HELIX_RUNTIME` environment variable.

### LSP isn't working

Is the LSP server in `$PATH`? If not, you will need to download it.