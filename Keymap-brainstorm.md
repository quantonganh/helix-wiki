Current keymap ([KLE](http://www.keyboard-layout-editor.com/#/gists/0e45da1f7e56b54c7f287551415b3fa8)):

![preview](https://user-images.githubusercontent.com/91177333/192541110-19a94459-9467-41f6-bbd8-56d02e99ba32.png)

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

# Note

From [`vision.md`](https://github.com/helix-editor/helix/blob/master/docs/vision.md#goals):
> - **Modal.**  Vim is a great idea.
> - **Selection -> Action**, not Verb -> Object.  Interaction models aren't linguistics, and "selection first" lets you see what you're doing (among other benefits).
> - **We aren't playing code golf.**  It's more important for the keymap to be consistent and easy to memorize than it is to save a key stroke or two when editing.

Start holding down a mod key (shift, ctrl, alt) is count as a keypress. Therefore we don't need a key combo that have the same keypress and do the same things as an existing key sequence, we only use a key combo for repeatable action.

<details>
<summary>E.g</summary>

| Example | Keypress |
| ------- | -------- |
| <kbd>a</kbd> | 1 |
| <kbd>A</kbd> | 2 |
| <kbd>a</kbd><kbd>b</kbd> | 2 |
| <kbd>A</kbd><kbd>A</kbd> = <kbd>shift down</kbd><kbd>a</kbd><kbd>a</kbd>_\[shift release\]_ | 3 |

</details>

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
|`C-.`|`C-n`    |
|`C-/`|`C-m`    |
|`C-<`|`C->`    |
|`C-/`|`C-KEYS` |
|`C-?`|`C-!`    |
|`C-@`|`C-^`    |
|`C-#`|`C-&`    |
|`C-$`|`C-*`    |
|`C-%`|`C-(`    |
|`C-)`|`C-_`    |
|`C-+`|`C-arrow`|
|`A--`|`A-nums` |
|`A-=`|`A-\`    |
|`A-_`|`A-a`    |
|`A-+`|`A-KEYS*`|
|`A-~`|`A-f`    |
|`A-q`|`A-g`    |
|`A-w`|`A-h`    |
|`A-e`|`A-j`    |
|`A-r`|`A-k`    |
|`A-t`|`A-l`    |
|`A-y`|`A-'`    |
|`A-u`|`A-"`    |
|`A-[`|`A-z`    |
|`A-]`|`A-v`    |
|`A-m`|`A-@`    |
|`A-/`|`A-#`    |
|`A-<`|`A-$`    |
|`A->`|`A-%`    |
|`A-?`|`A-\`    |
|`A-{`|`A-}`    |
|`A-^`|`A-*`    |
|`A-&`|`S-arrow`|
