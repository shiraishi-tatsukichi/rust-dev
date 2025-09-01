FROM docker.io/rustlang/rust:nightly-bookworm
ARG RUSTUP_TARGETS="wasm32-unknown-unknown x86_64-unknown-linux-gnu"
ARG RUSTUP_COMPONENTS="rustc cargo rustfmt rust-analyzer"
ARG BUILDER_USERNAME="builder"
ARG BUILDER_GROUPNAME=${BUILDER_USERNAME}
ARG BUILDER_UID="999"
ARG BUILDER_GID="999"

# builder グループ作成
RUN groupadd --system --gid ${BUILDER_GID} ${BUILDER_GROUPNAME}
# builder ユーザー作成
RUN useradd --system --uid ${BUILDER_UID} --gid ${BUILDER_GID} --shell /bin/bash ${BUILDER_USERNAME}

# rustup, cargo のディレクトリ所有権を builder:builder へ
RUN chown --recursive ${BUILDER_USERNAME}:${BUILDER_GROUPNAME} /usr/local/cargo && \
    chmod g+rw -R /usr/local/cargo && \
    chmod g+s /usr/local/cargo
RUN chown --recursive ${BUILDER_USERNAME}:${BUILDER_GROUPNAME} /usr/local/rustup && \
    chmod g+rw -R /usr/local/rustup && \
    chmod g+s /usr/local/rustup

USER ${BUILDER_USERNAME}
RUN rustup target add ${RUSTUP_TARGETS}
RUN rustup component add ${RUSTUP_COMPONENTS}

RUN curl -sSL https://github.com/cargo-bins/cargo-binstall/releases/latest/download/cargo-binstall-x86_64-unknown-linux-musl.tgz \
    | tar -xzf - -C /usr/local/cargo/bin cargo-binstall
RUN cargo binstall cargo-leptos -y
RUN cargo binstall wasm-opt -y
