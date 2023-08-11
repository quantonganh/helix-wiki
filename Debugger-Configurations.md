This page can provide additional debugger configurations beyond [the ones shipped by default in Helix](https://github.com/helix-editor/helix/blob/master/languages.toml).

## Install Debuggers

### lldb-vscode

#### macOS users

1. Install LLVM: `brew install llvm`
2. Add `/usr/local/opt/llvm/bin` your PATH, usually in your ~/.bashrc or .zshrc file.
3. Restart your shell

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
ln -s $(pwd)/codelldb_adapter/adapter/codelldb /usr/bin/codelldb
```

Test: `codelldb -h`

## Configure Debuggers

### Rust (with `lldb-vscode`)

Helix supports debugging Rust, by default, with [`lldb-vscode`](https://github.com/llvm/llvm-project/tree/main/lldb/tools/lldb-vscode), which is part of `llvm/lldb`.
However, there is an issue where [string variables are displayed as memory addresses instead of their actual values](https://github.com/helix-editor/helix/issues/7007).

To resolve this, [rust-lldb](https://github.com/rust-lang/rust/blob/master/src/etc/rust-lldb) provides a solution by executing specific lldb commands before loading the program:

```sh
$ rust-lldb target/debug/hello_cargo
(lldb) command script import "/opt/homebrew/Cellar/rust/1.71.0/lib/rustlib/etc/lldb_lookup.py"
(lldb) command source -s 0 '/opt/homebrew/Cellar/rust/1.71.0/lib/rustlib/etc/lldb_commands'
Executing commands in '/opt/homebrew/Cellar/rust/1.71.0/lib/rustlib/etc/lldb_commands'.
```

Once these commands are executed, the debugger can display the contents of local string variables:

```lldb
(lldb) b src/main.rs:5
Breakpoint 1: where = hello_cargo`hello_cargo::main::h24135e338b19c0c6 + 212 at main.rs:5:5, address = 0x0000000100003cc0
(lldb) run
Process 62497 launched: '/path/to/hello_cargo/target/debug/hello_cargo' (arm64)
Process 62497 stopped
* thread #1, name = 'main', queue = 'com.apple.main-thread', stop reason = breakpoint 1.1
    frame #0: 0x0000000100003cc0 hello_cargo`hello_cargo::main::h24135e338b19c0c6 at main.rs:5:5
   2        let s = "world";
   3        let x = 2;
   4        let b = true;
-> 5        println!("Hello, {} {} {}!", s, x, b);
   6    }
(lldb) frame variable
(&str) s = "world" {
  data_ptr = 0x0000000100039d70 "worldHello,  !\n"
  length = 5
}
(int) x = 2
(bool) b = true
(lldb)
```

Within `lldb-vscode`, we can replicate this functionality by using [initCommands](https://github.com/llvm/llvm-project/tree/main/lldb/tools/lldb-vscode#launch-configuration-settings):

```toml
[[language]]
name = "rust"

[language.debugger]
name = "lldb-vscode"
transport = "stdio"
command = "lldb-vscode"

[[language.debugger.templates]]
name = "binary"
request = "launch"
completion = [ { name = "binary", completion = "filename" } ]
args = { program = "{0}", initCommands = [ "command script import /opt/homebrew/Cellar/rust/1.71.0/lib/rustlib/etc/lldb_lookup.py", "command source -s 0 /opt/homebrew/Cellar/rust/1.71.0/lib/rustlib/etc/lldb_commands" ] }
```

### Rust (with `codelldb`)

You can also use [`vscode-lldb`](https://github.com/vadimcn/vscode-lldb)'s [adapter](https://github.com/vadimcn/vscode-lldb/tree/master/adapter) named `codelldb`. (Note, the names can be confusing. `vscode-lldb` is a separate project from the aforementioned `lldb-vscode`.)

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

2. Unpack the entire directory somewhere accessible in your system `$PATH` and create a symbolic link.

If you have `~/bin` in your path then unpack `LLVM` there and make a symlink to the `lldb-vscode` file that lives in the `bin` directory.

![Screenshot from 2022-10-12 19-43-46](https://user-images.githubusercontent.com/12832280/195423210-fea5970c-9453-4a8d-8acc-b0cfd5d626e6.png)

Now when you run the debugger in Helix select `launch debug target` and `binary`, then for example, to debug Rust, `target/debug/` and the name of your executable.

## Addendum 2: For users who installed a debugger successfully but cannot attach to a running process

If on Linux, trying to attach to a running process for debugging and being refused by the adapter due to a message similar to `Operation not permitted`, ensure `ptrace` is not blocking you. This can be done by following this [Microsoft troubleshooting guide](https://github.com/Microsoft/MIEngine/wiki/Troubleshoot-attaching-to-processes-using-GDB).

Summary of steps needed to be done are one of:
1. Ensure `/proc/sys/kernel/yama/ptrace_scope` has a `0` as value, instead of 1
2. If the file is not present or Yama is not used, use `libcap2-bin` to assign ptrace specific permissions to the debug adapter (overriding the command used by Helix, usually set in a `languages.toml` file).