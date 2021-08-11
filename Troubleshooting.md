* [Missing syntax highlighting](#missing-syntax-highlighting)
* [LSP isn't working](#lsp-isn-t-working)

### Missing syntax highlighting

Did you copy the `runtime` folder along with the `languages.toml` configuration file? By default, Helix will look for the runtime inside the same folder as the executable or in the config directory (Linux/MacOS: `~/.config/helix/` or `AppData/Roaming/Helix/` on Windows), but that can be overridden via the `HELIX_RUNTIME` environment variable.

### LSP isn't working

Is the LSP server (E.g. `rust-analyzer`) in `$PATH`?