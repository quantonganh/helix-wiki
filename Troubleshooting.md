### Missing syntax highlighting

If you are not using a package manager to install Helix, then you may have misplaced the required `runtime` folder. By default, it should be placed inside the same directory as the executable or [inside the system's config directory](https://docs.rs/dirs/4.0.0/dirs/fn.config_dir.html). This is `~/.config/helix/` on Linux/MacOS, and `~/AppData/Roaming/helix/` on Windows. However, this can be overridden by setting the `HELIX_RUNTIME` environment variable to your desired directory.

Additionally, check if the `runtime/grammars` folder contains the associated compiled tree-sitter grammar for the language. It should not be empty.

### LSP isn't working

Is the LSP server (E.g. `rust-analyzer`) in `$PATH`?

Try starting helix with the `-v` flag and [checking the log file](https://github.com/helix-editor/helix/wiki/FAQ#access-the-log-file) for LSP related messages.

### Failed to execute C compiler (building from source)

Both a C and a C++ compiler need to be installed.

### Rendering issues on MacOS terminal

The MacOS terminal lacks [true color support](https://gist.github.com/XVilka/8346728), so you'll need to install a terminal that has it.