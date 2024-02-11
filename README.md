# Native-TS

Thought of another idea, which I was contemplating recently. The original idea the other day was to make a way to compile JS to C, which would allow you to write "native JS". Then I decided to look into things further again.

https://www.reddit.com/r/rust/comments/uy1a3i/transpiling_typescript_into_rust/
https://github.com/benediktwerner/rewasm
https://users.rust-lang.org/t/any-interest-in-making-a-wasm-to-rust-transpiler/38880
https://stackoverflow.com/questions/56541790/is-it-possible-to-decompile-web-assembly-wasm-files-to-a-specific-programming
https://github.com/WebAssembly/wabt?tab=readme-ov-file

The new concept is that maybe I could transpile TS into Rust, which in turn would be able to compile down to native code. After searching for that, another really cool solution came up instead. You can compile both down to WebAssembly. So technically you could make a WebAssembly binary with something like AssemblyScript (TS), then decompile that into a Rust format of some sort, and maybe re-build that as a native binary, which doesn't even need a WebAssembly runtime. So I think the solution there, is that you'd essentially be using the Rust standard library for implementing the backing of your TS logic? In a weird way?

*Pantera - Vulgar Display Of Power*

---

Further exploration:

https://github.com/CryZe/wasm-to-rust
https://github.com/WebAssembly/wabt?tab=readme-ov-file (re-ref)
https://github.com/vshymanskyy/wasm2native
https://wasmer.io/posts/wasm-as-universal-binary-format-part-1-native-executables
https://github.com/wasmerio/wasmer
https://www.zksecurity.xyz/blog/posts/wasmati/
https://github.com/zksecurity/wasmati
https://www.reddit.com/r/typescript/comments/xdil0r/would_it_be_possible_to_create_a_compiler_to/

So I tried installing and both building/using the libraries I found above, but they either didn't build correctly on my machine, or if they did, then I discovered that the WASM produced by AssemblyScript requires the import of the APIs from the JS standard library, from the looks of it. So say like how my demo uses `console.log()`, it seems to just be importing that as a call into the WASM, rather than it being something part of the binary itself. It seems that's kind of like how some programs need the C++ redistributables on user systems. Those are shared libraries I think, right?

So I need to figure out a way of deciphering where JS standard librar features are referenced when using AssemblyScript, compared to being included as part of the build of the script itself. Maybe the other part is that this could possibly still work just right if I only use simple primitive things, like math and variables, rather than APIs like console logging.

```sh
brandon@hackbook:dist$ wasmer ./index.wasm
error: Unable to instantiate the WebAssembly module
╰─▶ 1: Error while importing "env"."console.log": unknown import. Expected Function(FunctionType { params: [I32], results: [] })

# this also errored
brandon@hackbook:dist$ wasmer create-exe ./index.wasm -o ./native-ts
```

*The Aristocrats - Tres Caballeros*