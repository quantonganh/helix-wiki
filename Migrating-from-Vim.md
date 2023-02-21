*Note:* As Helix is inspired by Vim and [Kakoune](https://github.com/mawww/kakoune), the keybindings are similar but has also some differences. The content of this page is inspired by [Kakoune Wiki](https://github.com/mawww/kakoune/wiki/Migrating-from-Vim).

NOTE: Unlike vim, `f`, `F`, `t` and `T` are not confined to the current line.

delete a word:
* vim: `dw`
* helix: `wd`

change a word:
* vim: `cw`
* helix: `ec` or `wc` (includes the whitespace after the word)

delete a character:
* vim: `x`
* helix: `d` or `;d`(`;` reduces the selection to a single char)

copy a line:
* vim: `yy`
* helix: `xy`

global replace:
* vim: `:%s/word/replacement/g<ret>`
* helix: `%sword<ret>creplacement<esc>`

Explanation: `%` selects the entire buffer, `s` opens a prompt for a regex, `<ret>` validates the regex and replace the selection with one per matches (hence, all occurences of word are selected). `c` deletes the selection contents and enter insert mode, replacement is typed and then `<esc>` goes back to normal mode.

go to last line:
* vim: `G`
* helix: `ge`

go to line start:
* vim: `0`
* helix: `gh`

go to line first non-blank character:
* vim: `^`
* helix: `gs`

go to line end:
* vim: `$`
* helix: `gl`

delete to line end:
* vim: `D`
* helix: `vgld` or `t<ret>d`

Note due to [go to line end does not select the text](https://github.com/helix-editor/helix/issues/1630
), `v` is required.

`t<ret>` selects "'til" the newline represented by `<ret>`.

jump to matching bracket:
* vim: `%`
* helix: `mm`

auto complete:
* vim: `C-p`
* helix: `C-x`

comment lines:
* vim: no keybinding by default. Using something like [vim-commentary](https://github.com/tpope/vim-commentary) adds this functionality
* helix: `C-c`

search for the word under the cursor:
* vim: `*`
* helix: `A-o*n` (if there's an LSP) or `be*n`

Explanation: if there's an LSP, `A-o` expands selection to the parent syntax node (with would be the word in our case). Then `*` uses the current selection as the search pattern, and `n` goes to the next occurence. `be` selects to the begining of the word, and `e` selects to the end of the word, effectively selecting the whole word.

block selection:
* vim: `C-v`, then expand your selection vertically and horizontally
* helix: There's no "block selection" mode, so instead you'd use multiple cursors. Expand your block selection vertically by adding new cursors on the line below with `C`, and horizontally using standard movements

search "foo" and replace with "bar" in the current selection:
* vim: `:s/foo/bar/g<ret>`
* helix: `sfoo<ret>cbar<esc>,`

Explanation: `s` will open a prompt in the command line for a regex, and select all matches inside the selection (effectively adding a new cursor on each match). Pressing enter will then finalise this step, and allow the `c` to change the selections to "bar". When done, go back to normal mode with `<esc>`, and keep only the primary selection with `,` (remove all the additional cursors).

select the whole file:
* vim: `ggVG`
* helix: `%`

reload a file from disk:
* vim: `:e<ret>`
* helix: `:reload<ret>` (or `:reload-all<ret>` to reload all the buffers)

Helix enables easy movement in `insert` mode without switching to `normal` mode. When in `insert` mode, you can use the same set of keybindings as in [GNU Readline Emacs Key Binding](https://en.wikipedia.org/wiki/GNU_Readline#Emacs_keyboard_shortcuts). Such as `Ctrl-b`, `Ctrl-f`, `Alt-b`, `Alt-f`, `Ctrl-d`, `Alt-d`, `Ctrl-a`, `Ctrl-e`. For more, you can see the [book](https://docs.helix-editor.com/keymap.html#insert-mode). So if you are previously an Emacs user, or used this keybindings in the Bash/Zsh shell, or on macOS, you should feel at home in Helix.


