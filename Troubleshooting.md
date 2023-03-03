### Missing syntax highlighting

If you haven't already you should check out the [helix healthcheck](https://github.com/helix-editor/helix/wiki/Healthcheck). Running `hx --health <lang>` for a language must print a checkmark for the "Highlight queries" section in order for highlights to work.

If you are not using a package manager to install Helix, then you may have misplaced the required `runtime` folder. By default, it should be placed inside the same directory as the executable or [inside the system's config directory](https://docs.rs/dirs/4.0.0/dirs/fn.config_dir.html). This is `~/.config/helix/` on Linux/MacOS, and `~/AppData/Roaming/helix/` on Windows. However, this can be overridden by setting the `HELIX_RUNTIME` environment variable to your desired directory.

Additionally, check if the `runtime/grammars` folder contains the associated compiled tree-sitter grammar for the language. It should not be empty. If it is, then run `hx --grammar fetch` and `hx --grammar build`.

Finally, you can open a file for the language missing syntax highlighting, and check your logs with `:log-open`.

### LSP isn't working

Features like auto-complete, diagnostics, and goto-definition are driven by LSP. You must have a language's language server installed for these features to work.

If you haven't already you should check out the [helix healthcheck](https://github.com/helix-editor/helix/wiki/Healthcheck). Running `hx --health <lang>` for a language must print the language server executable name in green in the "Configured language server" section. Make sure the language server executable is in `$PATH`.

If the language server is installed, try starting helix with the `-v` flag and [checking the log file](https://github.com/helix-editor/helix/wiki/FAQ#access-the-log-file) for LSP related messages.

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

Neither `Space-p` nor `Space-y` is working.

#### On Linux

In an X session, check that either the [`xclip`](https://repology.org/project/xclip/versions) or [`xsel`](https://repology.org/project/xsel/versions) package is installed on your system and either of these commands is in your `PATH`.

In a Wayland session, check that the [`wl-clipboard`](https://repology.org/project/wl-clipboard/versions) package is installed on your system and the provided `wl-copy` and `wl-paste` commands are in your `PATH`.

#### On WSL

Check that `win32yank.exe` is in your Windows path.

Either download the [binaries](https://github.com/equalsraf/win32yank/releases/tag/v0.0.4) manually or use scoop (`scoop install win32yank`).

### Panic from "Could not parse queries" (building from source)

You may encounter a panic when opening a file that looks like so:

```
thread 'main' panicked at 'Could not parse queries for language "<language>". Are your grammars out of sync? Try running 'hx --grammar fetch' and 'hx --grammar build'. This query could not be parsed: QueryError { row: 0, column: 17, offset: 17, message: "heading_content", kind: NodeType }', helix-core/src/syntax.rs:377:43
```

This happens when the tree-sitter queries (`.scm` files) in your `~/.config/helix/runtime/queries` directory are out of date with the tree-sitter parsers. To fix this, remove the `~/.config/helix/runtime` directory and [link the runtime directory](https://github.com/helix-editor/helix/blob/7711db3a3af8f7ca156c8c71ae4b7ea2dd02d96f/README.md?plain=1#L48-L55) from this repository. Then run `hx -g fetch` and `hx -g build`.
