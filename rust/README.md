# rust wasi demo

## Steps

### 1. Add wasi target
```
$ rustup target add wasm32-wasi
```

[How to install rust](https://www.rust-lang.org/tools/install)

### 2. Build
```
$ rustc --target wasm32-wasi main.rs
```

### 3. Run
```
$ wasmtime main.wasm
```

[How to install wasmtime](https://wasmtime.dev/)
