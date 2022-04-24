### Missing syntax highlighting

If you are not using a package manager to install Helix, then you may have misplaced the required `runtime` folder. By default, it should be placed inside the same directory as the executable or [inside the system's config directory](https://docs.rs/dirs/4.0.0/dirs/fn.config_dir.html). This is `~/.config/helix/` on Linux/MacOS, and `~/AppData/Roaming/helix/` on Windows. However, this can be overridden by setting the `HELIX_RUNTIME` environment variable to your desired directory.

Additionally, check if the `runtime/grammars` folder contains the associated compiled tree-sitter grammar for the language. It should not be empty.

### LSP isn't working

Is the LSP server (E.g. `rust-analyzer`) in `$PATH`?

Try starting helix with the `-v` flag and [checking the log file](https://github.com/helix-editor/helix/wiki/FAQ#access-the-log-file) for LSP related messages.

#### On Windows

If you are on PowerShell, try these steps:
- Check if the LSP server is available first by running `gcm <lsp-command-name>`. If you are unsure which LSP server is powering the language that you are using, then please refer to [languages.toml](https://github.com/helix-editor/helix/blob/master/languages.toml). Upon running this command, you would see an output like this:

![Image showing output of gcm command](https://i.imgur.com/cJmVLCy.png) 

- Under Name column, notice the extension of these files. `rust-analyzer` ends with `.exe`, which is great, as it would work out of the box. But `typescript-language-server` ends with `.ps1`. In this case we would try to find a server file with `.cmd` extension:

![output of `gcm typescript-language-server.cmd` showing that the corresponding file is available](https://i.imgur.com/SV86JLp.png)

- That's good, we do have a `.cmd` file with us. We would use this filename as our LSP server for TypeScript. Open `languages.toml` file and type this in (you could find it in C:\Users\\[username]\AppData\Roaming\helix\languages.toml, if it isn't present then create one):

```toml
[[language]]
name = "typescript"
language-server.command = "typescript-language-server.cmd"
```

- Once you save the above file, close Helix and try to open your project again. Open the file you are expecting for LSP to work in. Within few seconds,  Helix would be giving you errors and autocompletion.

### Failed to execute C compiler (building from source)

Both a C and a C++ compiler need to be installed.

### Rendering issues on MacOS terminal

The MacOS terminal lacks [true color support](https://gist.github.com/XVilka/8346728#terminal-emulators), so you'll need to install a terminal that has it.

### When using tmux or screen, there is a delay after hitting Escape before it's registered

This is because your terminal multiplexer is listening for escape keypresses itself, as part of its own escape sequences, and only passing them to Helix after a delay when it's stopped listening for more keypresses in the sequence.
So when you press escape to return to normal mode in Helix, the terminal multiplexer catches it, and only passes it to Helix after the delay. 

For changing or disabling the timeout, both tmux.conf and screenrc accept a timeout in milliseconds.

If you don't use escape in your tmux or screen escape sequences, you can disable it:
- For tmux.conf (`~/.tmux.conf` or `/etc/tmux.conf`), add `set -sg escape-time 0`
- For screenrc (`~/.screenrc` or `/etc/screenrc`), `maptimeout 0`

You can also set the timeout to a low value instead:
- For tmux.conf, `set -sg escape-time 10`
- For screenrc, `maptimeout 10`

For why this doesn't appear to happen in Neovim and Vim, see: https://github.com/neovim/neovim/wiki/FAQ#esc-in-tmux-or-gnu-screen-is-delayed

### Copy/paste from/to system clipboard not working
Neither `Space-p` nor `Space-Y` is working.
#### On Linux
Check that `xsel` package is installed in your system.