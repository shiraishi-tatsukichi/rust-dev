FROM docker.io/rustlang/rust:nightly-bookworm
ARG RUSTUP_TARGETS="wasm32-unknown-unknown x86_64-unknown-linux-gnu"
RUN rustup target add ${RUSTUP_TARGETS}

RUN curl -sSL https://github.com/cargo-bins/cargo-binstall/releases/latest/download/cargo-binstall-x86_64-unknown-linux-musl.tgz \
    | tar -xzf - -C /usr/local/cargo/bin cargo-binstall
RUN cargo binstall cargo-leptos --locked -y
RUN cargo binstall wasm-opt --locked -y
