Current keymap:

[![Preview](https://user-images.githubusercontent.com/43980777/140440280-dcc31d86-c87d-46d1-8bb3-d1c6d9610c92.png)](http://www.keyboard-layout-editor.com/#/gists/fb432523c4e62a6d3babfdaa0152b5d0)

We are still thinking about visual mode and there are some issues with kakoune and vim that we want to address.

vim
- we think a visual first is better (multi-cursors support)

kakoune
- we don't want to hold `shift` for extend
- we don't want to use `alt`

both
- we don't want to hold `ctrl-f` to page down (should be like in `V` kakoune as pager)
- keep visual, linewise visual, visual block mode in vim while having the ability to be visual first
- we prefer not to hold keys (shift, ctrl, alt)

Cases below may not be able to utilize lsp functions. Should be real cases for normal workflow. Commenting functions also won't be useful.

We want to provide one way without using count and one way using count since we may not always use count. Keystrokes count, pressing shift is considered a count.

# Sample one

```rust
/// ```
/// impl EditorView {
///     pub fn new() -> Self {
///         Self {
///             keymap: keymap::default(),
///             on_next_key: None,
///             last_insert: (commands::normal_mode, Vec::new()),
///             completion: None,
///         }
///     }
/// ```
```

## Case one

Delete the whole line starting from `Self {` to `}` (including last newline), cursor starts at `/// (#)` on line `Self {`. 

vim
- @pickfire `V%d` (5), with count `6dd` (3)
- @CBenoit `V%d` is (4) not (5)

kakoune
- @pickfire `ghMLd` (6), with count `6Xd` (4)
- @vbauerster `m<a-x>d` (4)

helix
- @pickfire `Vmvld` (6) if we follow vim, with count (current) `ghV5jgld` (9), with count (current + X) `ghV5Xd` (8)
- @CBenoit with helix line-wise extend mode (like in vim), we should get `Vmd` (4) without count and `V5jd` (5) with count.

## Case two

Add line comment before `Self {` to matching `}` all on same column, starting at `Self {`.

vim
- @pickfire `ctrl-vI// ` (7)

kakoune
- @pickfire `CCCCCi// ` (10) - I wish there is a better way, with count `5Ci// ` (7)
- @vbauerster `m<a-s>ghi//`

helix
- @pickfire maybe we need to have visual block?

Err, maybe we should count escape key?

- TODO swapping key value position in code
- TODO xml editing, joining child, removing parent, splitting child, swapping key position
- TODO (rare use cases) drawing boxes
- TODO I noticed that helix requires a lot more keys just to change till end of line (not including newline)

Reference:
- https://github.com/mawww/kakoune/blob/master/doc/pages/keys.asciidoc#object-selection (@archseer initial design based on this)

---

# Suggestions
These are some keys which can be re-mapped without clashes with other commands.

### Normal Mode

```
nums: `1 2 3 4 5 6 7 8 9 0`
arrow: `left right up down`
KEYS: All captial alphabet keys
KEYS*: All KEYS other than U, K and C
```

> DISCLAIMER: Might be outdated. Last edited as of 20th November, 2021.

|Keys|Keys|
|--|--|
|`H`  |`M`      |
|`@`  |`C-~`    |
|`#`  |`C-nums` |
|`^`  |`C--`    |
|`-`  |`C-=`    |
|`+`  |`C-q`    |
|`\`  |`C-e`    |
|`.`  |`C-r`    |
|`D`  |`C-t`    |
|`L`  |`C-y`    |
|`V`  |`C-p`    |
|`C-j`|`C-[`    |
|`C-k`|`C-]`    |
|`C-l`|`C-\`    |
|`C-;`|`C-{`    |
|`C-'`|`C-}`    |
|`C-:`|`C-\|`    |
|`C-"`|`C-g`    |
|`C-v`|`C-h`    |
|`C-b`|`C-.`    |
|`C-n`|`C-/`    |
|`C-m`|`C-<`    |
|`C->`|`C-arrow`|
|`C-/`|`C-KEYS` |
|`C-?`|`C-!`    |
|`C-@`|`C-^`    |
|`C-#`|`C-&`    |
|`C-$`|`C-*`    |
|`C-%`|`C-(`    |
|`C-_`|`C-+`    |
|`A--`|`A-nums` |
|`A-=`|`A-\`    |
|`A-_`|`A-a`    |
|`A-+`|`A-d`    |
|`A-~`|`A-f`    |
|`A-q`|`A-g`    |
|`A-w`|`A-h`    |
|`A-e`|`A-j`    |
|`A-r`|`A-k`    |
|`A-t`|`A-l`    |
|`A-y`|`A-:`    |
|`A-u`|`A-'`    |
|`A-i`|`A-"`    |
|`A-o`|`A-z`    |
|`A-p`|`A-x`    |
|`A-[`|`A-c`    |
|`A-]`|`A-v`    |
|`A-n`|`A-KEYS*` |
|`A-m`|`A-@`    |
|`A-/`|`A-#`    |
|`A-<`|`A-$`    |
|`A->`|`A-%`    |
|`A-?`|`A-\`    |
|`A-{`|`A-}`    |
|`A-^`|`A-*`    |
|`A-&`|`A-arrow`|
|`S-arrow`|`C-arrow`|
