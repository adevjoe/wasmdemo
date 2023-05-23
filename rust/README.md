# rust wasi demo

## Steps

### 1. Add wasi target
```
$ rustup target add wasm32-wasi
```

[How to install rust](https://www.rust-lang.org/tools/install)

### 2. Build
```
$ cargo build --target wasm32-wasi
```

`wasm` file will place in `target/wasm32-wasi/debug` dir.

### 3. Run
```
$ wasmtime target/wasm32-wasi/debug/rust.wasm
```

[How to install wasmtime](https://wasmtime.dev/)
