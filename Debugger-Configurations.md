This page can provide additional debugger configurations beyond [the ones shipped by default in Helix](https://github.com/helix-editor/helix/blob/master/languages.toml).


## Rust (with `codelldb`)

Helix supports debugging Rust, by default, with [`lldb-vscode`](https://github.com/llvm/llvm-project/tree/main/lldb/tools/lldb-vscode), which is part of `llvm/lldb`.

However, you can also use [`vscode-lldb`](https://github.com/vadimcn/vscode-lldb)'s [adapter](https://github.com/vadimcn/vscode-lldb/tree/master/adapter) named `codelldb`. (Note, the names can be confusing. `vscode-lldb` is a separate project from the aforementioned `lldb-vscode`.)

```toml
[[language]]
name = "rust"

[language.debugger]
command = "codelldb"
name = "codelldb"
port-arg = "--port {}"
transport = "tcp"

[[language.debugger.templates]]
name = "binary"
request = "launch"
[[language.debugger.templates.completion]]
completion = "filename"
name = "binary"

[language.debugger.templates.args]
program = "{0}"
runInTerminal = true
```

Test with: `debug-start binary target/debug/zellij`, for example.
Status: start/stop debugging works, breakpoints work