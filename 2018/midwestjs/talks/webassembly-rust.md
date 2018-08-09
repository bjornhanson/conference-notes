# WebAssembly with Rust
- Speaker: [Robert Hanson](https://github.com/kimtuck)
- [Presentation repo](https://github.com/kimtuck/webassembly)

## Notes

Rust won first place for "most loved programming language" in Stack Overflow's developer survey in 2016, 2017, 2018.

Rust gained browser support by most major browsers in 2017 (it's new).

If you look into WebAssembly, most people are using Rust.

### What is WebAssembly
- WebAssembly is a compilation target (compile down to it from another language)
- Binary format (with a textual representation in dev tools)
- Runs inside a VM, but can stream and start running before finished loading
- The compiled `.wasm` file is an asset, just like a `.js` or `.png` file for your site
- Loads fast
- Runs at native speed
- Single-threaded (same as UI thread)
- Can talk to JavaScript code

Use it for things you don't want to do in JS:
- Physics engine
- Image processing
- CPU emulator
- Synthesizer
- Render CAD drawings

There are probably already Rust (or C, or C++) libraries you can use.

Reasons to use WebAssmebly:
- Protect your core business logic
- Computational intensive operations
- Encryption

High-level language options
- Rust
- C, C++ --emscripten
- [Many more](http://github.com/appcypher/awesome-wasm-langs)
- Requirements: no garbage collection; no exceptions thrown

JavaScript API
- [Difficult-to-read description](http://developer.mozilla.org/en-US/docs/WebAssembly/Using_the_JavaScript_API)
- Only two integer types and two floating point types
- `wasm-bindgen` is helpful - automatically generates the glue code, by inspecting your Rust code. Makes it appear to be able to manipulate the DOM, though it technically can't.

### What is Rust
- Compiles directly to WebAssembly
- Can compile to many different target platforms (Windows, Linux, iOS, Android, etc.)

Language features:
- No garbage collection
- No exceptions
- Guaranteed memory safety; no null/dangling pointers
- Ownership, borrowing
- Easy unit testing
- Fearless threading
- Higher-level language constructs, generics, traits
- npm-like open source packages - "cargo" and "crates"
- Comprehensive build system
- Native code for many enviornments
- Is statically typed

### Installation/getting started
- [Install Rust](https://www.rust-lang.org/en-US/install.html)
- `rustup default nightly`
- `rustup target add wasm32-unknown-unknown --toolchain nightly`
- Install wasm-bingen library in each project: `cargo +nightly install wasm-bindgen-cli --force`

### Examples


## Resources
- [Rust](https://www.rust-lang.org)
- [WebAssembly](https://webassembly.org)
- [Wasm-bindgen](https://github.com/rustwasm/wasm-bindgen)
- https://hacks.mozilla.org/2018/04/javascript-to-rust-and-back-again-a-wasm-bindgen-tale/
