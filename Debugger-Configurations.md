This page can provide additional debugger configurations beyond [the ones shipped by default in Helix](https://github.com/helix-editor/helix/blob/master/languages.toml).

## Install Debuggers
### Codelldb [![GitHub release (latest by date)](https://img.shields.io/github/v/release/vadimcn/vscode-lldb)](https://github.com/vadimcn/vscode-lldb/releases/)
`linux (tested in ubuntu)`: 

Access your user folder.
```sh
cd ~
```

Check the architecture of the cpu to later download the correct version of `codelldb`.
```sh
lscpu | grep -oP 'Architecture:\s*\K.+'
```

create a folder named `bin` and access it.
```sh
mkdir bin && cd bin
```

Will download `codelldb` through `curl`. ( `.vsix` can be opened as `.zip` ).
```sh
sudo curl -L "https://github.com/vadimcn/vscode-lldb/releases/download/v1.7.0/codelldb-x86_64-linux.vsix" -o "codelldb-x86_64-linux.zip"
```

Unzip only the necessary folders, in this case `extension/adapter` and `extension/lldb`.
```sh
unzip "codelldb-x86_64-linux.zip" "extension/adapter/*" "extension/lldb/*"
```

Rename the `extension/` folder to `codelldb_adapter/`
```sh
mv extension/ codelldb_adapter
```

Delete the unneeded `codelldb-x86_64-linux.zip` at this time.
```sh
sudo rm "codelldb-x86_64-linux.zip"
```

Create the symlink from `codelldb_adapter/adapter/codelldb` to `/usr/bin/codelldb` and you're done.
```sh
ln codelldb_adapter/adapter/codelldb /usr/bin/codelldb
```

Test: `codelldb -h`

## Configure Debuggers
### Rust (with `codelldb`)

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

## Addendum: For users who can't make any of the above work

To simply install the default debugger that will work out of the box you need to:

1. Install `LLVM`.

The easiest way to do this is to use the pre-compiled binaries from the releases page: https://github.com/llvm/llvm-project/releases, for example, at the time of writing the latest version for Linux is: https://github.com/llvm/llvm-project/releases/download/llvmorg-15.0.2/clang+llvm-15.0.2-x86_64-unknown-linux-gnu-rhel86.tar.xz

2. Unpack the entire directory somewhere accessible in your system `$PATH` and create a symbolic link

If you have `~/bin` in your path then unpack `LLVM` there and make a symlink to the `lldb-vscode` file that lives in the `bin` directory.

![Screenshot from 2022-10-12 19-43-46](https://user-images.githubusercontent.com/12832280/195423210-fea5970c-9453-4a8d-8acc-b0cfd5d626e6.png)

Now when you run the debugger in Helix select `launch debug target` and `binary`, then for example, to debug Rust, `target/debug/` and the name of your executable.