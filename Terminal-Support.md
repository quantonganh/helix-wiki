Helix requires a fairly modern terminal for things like [truecolor support](https://github.com/termstandard/colors). Helix also uses some optional terminal features to enhance its operation. The terminals in this table all meet Helix's basic requirements. The table summarizes their support for the optional features.

|           |[Focus Events]|[Bracketed Paste]|[Set OS Clipboard]|[Extended Underlines]|[Enhanced Keyboard Protocol]|
|-----------|--------------|-----------------|------------------|---------------------|----------------------------|
|[Alacritty]| ✅           | ✅              | ✅               | 🆗 (partial)        | ❌                         |
|[Kitty]    | ✅           | ✅              | ✅               | ✅                  | ✅                         |
|[Wezterm]  | ✅           | ✅              | ✅               | ✅                  | ✅ (with config)           |

[Focus Events]: #focus-events
[Bracketed Paste]: #bracketed-paste
[Set OS Clipboard]: #set-os-clipboard
[Extended Underlines]: #extended-underlines
[Enhanced Keyboard Protocol]: #enhanced-keyboard-protocol
[Alacritty]: #alacritty
[Kitty]: #kitty
[Wezterm]: #wezterm

## Unsupported Terminals

These terminals don't meet the basic requirements:
* [Apple's Terminal.app](#terminalapp)

### Chinese, Japanese and Korean script

These terminals have been reported to exhibit rendering issues for CJK characters on Windows:

* PowerShell ([#5753](https://github.com/helix-editor/helix/issues/5753))
* Alacritty ([#5753 comment](https://github.com/helix-editor/helix/issues/5753#issuecomment-1411461592))

Wezterm has been recommended for use on Windows in response.

## Adding terminals

If a terminal isn't in the table, it doesn't mean that Helix doesn't work in it, just that no one has tested it. To add a terminal, please add an entry for it to the [terminals section](#terminals) with the version you used and when you tested.

# Terminal Features

## Focus Events

[Focus events](https://terminalguide.namepad.de/mode/p1004/) can be emitted by a terminal when it gains or loses focus at the OS level.
[3178](https://github.com/helix-editor/helix/pull/3178) added an option to save when it loses focus.

## Bracketed Paste

[Bracketed paste](https://en.wikipedia.org/wiki/Bracketed-paste) lets a terminal tell an application that incoming characters are from the user pasting, not from typing.
[3233](https://github.com/helix-editor/helix/pull/3233) keeps pasted text from being autoformatted making pasting much faster.

## Set OS Clipboard

[Set clipboard](https://terminalguide.namepad.de/seq/osc-52/) lets an application running in a terminal set the clipboard in the surrounding OS.
Helix supports setting the system clipboard with the "yank selection to clipboard" command, which is bound to `space y` by default.

When Helix is running directly on an OS that supports setting the clipboard, it'll use the OS's facilities to set the clipboard.
That's `xclip` in X Windows, `wl-copy` on Wayland, `pbcopy` on MacOS, and direct API access on Windows.

On systems where that isn't availble, Helix will use this terminal feature to set the clipboard when [3220](https://github.com/helix-editor/helix/pull/3220) lands.
For example if you're SSH'd into a remote host, Helix will be able to set your OS clipboard if your terminal supports this feature.

## Extended Underlines

Some terminals support [Kitty's extended underlines.](https://sw.kovidgoyal.net/kitty/underlines/)

## Enhanced Keyboard Protocol

Some terminals support [Kitty's progressive keyboard enhancement protocol.](https://sw.kovidgoyal.net/kitty/keyboard-protocol/). The enhanced keyboard protocol disambiguates the escape sequences for some keyboard events that are impossible to tell apart by default. For example the `C-i` key combination sends the same escape sequences to Helix as the Tab key and `C-backspace` sends the same escape sequences as `C-h`.

You can check if the enhanced keyboard protocol is supported by your terminal emulator and Helix by checking the [log file] when running in verbose mode with `hx -vv`. Helix versions with enhanced keyboard protocol support will print a debug line on start-up saying either "The enhanced keyboard protocol is supported on this terminal" or "The enhanced keyboard protocol is not supported on this terminal". If neither of those lines exist, you should use a newer version of Helix.

The enhanced keyboard protocol must be explicitly enabled in WezTerm. See https://wezfurlong.org/wezterm/config/key-encoding.html#kitty-keyboard-protocol.

[log file]: https://github.com/helix-editor/helix/wiki/FAQ#access-the-log-file

# Terminals

## Alacritty

[Alacritty](https://alacritty.org/) was tested using version 0.10.0 on 2022-08-11.

## Kitty

[Kitty](https://sw.kovidgoyal.net/kitty/) was tested using version 0.25.2 on 2022-08-11.

## Wezterm

[Wezterm](https://wezfurlong.org/wezterm/) was tested using version 20220807-113146-c2fee766 on 2022-08-11.

# Unsupported Terminals

## Terminal.app

As of version 2.12.7 (445) on Mac OS 12.5, it doesn't support [truecolor](https://github.com/termstandard/colors).
