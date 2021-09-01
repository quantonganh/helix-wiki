* [Missing syntax highlighting](#missing-syntax-highlighting)
* [LSP isn't working](#lsp-isn-t-working)

### Missing syntax highlighting

Did you configure the location of the the `runtime` folder? By default, Helix will look for the runtime inside the same folder as the executable or in the config directory (Linux/MacOS: `~/.config/helix/` or `AppData/Roaming/Helix/` on Windows), but that can be overridden via the `HELIX_RUNTIME` environment variable. (This is only required if building from source, packaged releases by distributions already handle this for you by specifying the HELIX_RUNTIME variable)

### LSP isn't working

Is the LSP server (E.g. `rust-analyzer`) in `$PATH`?