# How to add Rust LSP:
- Use the following commands to install rust-analyzer into `~/.local/bin`:
```sh
curl -L https://github.com/rust-analyzer/rust-analyzer/releases/latest/download/rust-analyzer-x86_64-unknown-linux-gnu.gz | gunzip -c - > ~/.local/bin/rust-analyzer
```
```sh
chmod +x ~/.local/bin/rust-analyzer
```
__Run them separately!!
Make sure that `~/.local/bin` is there in $PATH.
If not, see this wiki.__

> Go to this [site](https://rust-analyzer.github.io/manual.html#rust-analyzer-language-server-binary) for more info.

#### Helix will automatically run the `rust-analyzer`.
