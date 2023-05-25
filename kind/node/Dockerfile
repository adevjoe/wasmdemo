ARG KIND_NODE_VERSION=v1.24.12

# Base image
FROM kindest/node:${KIND_NODE_VERSION} AS kind-base

# Build containerd shim
FROM kind-base AS shim-build

## Install rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > /tmp/rustup.sh && sh /tmp/rustup.sh -y --profile=minimal
ENV PATH="/root/.cargo/bin:${PATH}"
RUN rustup install stable
WORKDIR /shim

## Install WasmEdge
RUN apt-get update && apt-get install --no-install-recommends -y build-essential git clang pkg-config libsystemd-dev libdbus-glib-1-dev build-essential libelf-dev libseccomp-dev libclang-dev
RUN curl -sSf https://raw.githubusercontent.com/WasmEdge/WasmEdge/master/utils/install.sh | bash -s -- --version=0.12.1

## Build runwasi and install shim
RUN git clone https://github.com/containerd/runwasi.git
RUN \
    --mount=type=cache,target=/usr/local/cargo/registry \
    --mount=type=cache,target=/shim/target \
    cd runwasi; mkdir -p /opt/shim; make build install PREFIX=/opt/shim

# Copy shim
FROM scratch AS shim
COPY --from=shim-build /opt/shim/bin/* /

# Build kind node image
FROM kind-base

## change containerd config
RUN <<EOF
set -e
echo '[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.wasm]' >> /etc/containerd/config.toml
echo 'runtime_type = "io.containerd.wasmtime.v1"' >> /etc/containerd/config.toml
sed -i 's,SystemdCgroup = true,,' /etc/containerd/config.toml
EOF
COPY --link --from=shim /* /usr/local/bin/
