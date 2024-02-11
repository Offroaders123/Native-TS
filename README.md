# Native-TS

Thought of another idea, which I was contemplating recently. The original idea the other day was to make a way to compile JS to C, which would allow you to write "native JS". Then I decided to look into things further again.

https://www.reddit.com/r/rust/comments/uy1a3i/transpiling_typescript_into_rust/
https://github.com/benediktwerner/rewasm
https://users.rust-lang.org/t/any-interest-in-making-a-wasm-to-rust-transpiler/38880
https://stackoverflow.com/questions/56541790/is-it-possible-to-decompile-web-assembly-wasm-files-to-a-specific-programming
https://github.com/WebAssembly/wabt?tab=readme-ov-file

The new concept is that maybe I could transpile TS into Rust, which in turn would be able to compile down to native code. After searching for that, another really cool solution came up instead. You can compile both down to WebAssembly. So technically you could make a WebAssembly binary with something like AssemblyScript (TS), then decompile that into a Rust format of some sort, and maybe re-build that as a native binary, which doesn't even need a WebAssembly runtime. So I think the solution there, is that you'd essentially be using the Rust standard library for implementing the backing of your TS logic? In a weird way?

*Pantera - Vulgar Display Of Power*