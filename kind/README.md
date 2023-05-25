# Run WASI in k8s

## 1. Install Kind

[How install kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

## 2. Build kind node image

```shell
$ docker build --push -t ghcr.io/adevjoe/kind-wasm:v1.24.12 node
```

## 3. Create cluster

```shell
$ kind create cluster --config=wasm.yaml --name=wasm
```

## 4. Create Runtime Class

```shell
$ kubectl apply -f runtime.yaml
```

## 5. Demo

```shell
$ kubectl apply -f job.yaml
```
