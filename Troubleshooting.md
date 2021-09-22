### Missing syntax highlighting

Did you configure (or copy from source code) the location of the the `runtime` folder **within** config directory (like `~/.config/helix/runtime/`)? By default, Helix will look for the runtime inside the same folder as the executable or in the config directory (Linux/MacOS: `~/.config/helix/` or `AppData/Roaming/Helix/` on Windows), but that can be overridden via the `HELIX_RUNTIME` environment variable. (This is only required if building from source, packaged releases by distributions already handle this for you by specifying the HELIX_RUNTIME variable)

### LSP isn't working

Is the LSP server (E.g. `rust-analyzer`) in `$PATH`?

Try starting helix with the `-v` flag and checking the log file (`~/.cache/helix/helix.log`) for LSP related messages.

### Failed to Execute C Compiler (building from source)

Both a C and a C++ compiler need to be installed.