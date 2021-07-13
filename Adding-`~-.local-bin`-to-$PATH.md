# How to add `~/.local/bin` to $PATH:
> Check if `~/.local/bin` in there in your path by: `echo $PATH`

- Open your shell rc (eg: `.bashrc`, `.zshrc`, etc) in your preferred editor.
- Go to the end of the file (`ge` in Helix).
- Type:
```sh
export $PATH=$PATH:$HOME/.local/bin
```
- Source your shell (`. ~/.zshrc` OR `. ~/.bashrc`).

> Congrats! You can now proceed with [this](https://github.com/helix-editor/helix/wiki/How-to-add-an-LSP)!