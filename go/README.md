# go wasi demo

## Steps

### 1. Install gotip
```
$ go install golang.org/dl/gotip@latest
$ gotip download
```

or use [tinygo](https://tinygo.org/)

### 2. Build
```
$ GOOS=wasip1 GOARCH=wasm gotip build -o main.wasm main.go
```

or
```
$ tinygo build -target=wasi -o main.wasm main.go
```

### 3. Run
```
$ wasmtime main.wasm
```

[How to install wasmtime](https://wasmtime.dev/)
