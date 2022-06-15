*Note:* As Helix is inspired by Vim and [Kakoune](https://github.com/mawww/kakoune), the keybindings are similar but has also some differences. The content of this page is inspired by [Kakoune Wiki](https://github.com/mawww/kakoune/wiki/Migrating-from-Vim).

NOTE: Unlike vim, `f`, `F`, `t` and `T` are not confined to the current line.

delete a word:
* vim: `dw`
* helix: `wd`

delete a character:
* vim: `x`
* helix: `d` or `,d`(`,` reduces the selection to a single char)

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

auto complete:
* vim: `C-p`
* helix: `C-x`

Helix enables easy movement in `insert` mode without switching to `normal` mode. When in `insert` mode, you can use the same set of keybindings as in [GNU Readline Emacs Key Binding](https://en.wikipedia.org/wiki/GNU_Readline#Emacs_keyboard_shortcuts). Such as `Ctrl-b`, `Ctrl-f`, `Alt-b`, `Alt-f`, `Ctrl-d`, `Alt-d`, `Ctrl-a`, `Ctrl-e`. More can see the [book](https://docs.helix-editor.com/keymap.html#insert-mode). So if you are previously an Emacs user, or used this keybindings in the Bash/Zsh shell, or on macOS, you should feel at home in Helix.


