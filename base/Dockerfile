FROM docker.io/rustlang/rust:nightly-bookworm
ARG RUSTUP_TARGETS="wasm32-unknown-unknown x86_64-unknown-linux-gnu"
ARG DEVS_GROUPNAME="devs"
ARG DEVS_GID="999"
ARG BUILDER_USERNAME="builder"
ARG BUILDER_UID="998"

# devs グループ作成
RUN groupadd --system --gid ${DEVS_GID} ${DEVS_GROUPNAME}
# builder ユーザー作成
RUN useradd --system --uid ${BUILDER_UID} --shell /bin/bash ${BUILDER_USERNAME} &&\
    usermod --append --groups ${DEVS_GROUPNAME} ${BUILDER_USERNAME}

RUN chown ${BUILDER_USERNAME}:${DEVS_GROUPNAME} /usr/local/cargo &&\
    chmod g+s /usr/local/cargo
RUN chown ${BUILDER_USERNAME}:${DEVS_GROUPNAME} /usr/local/rustup &&\
    chmod g+s /usr/local/rustup

USER ${BUILDER_USERNAME}
RUN rustup target add ${RUSTUP_TARGETS}

RUN curl -sSL https://github.com/cargo-bins/cargo-binstall/releases/latest/download/cargo-binstall-x86_64-unknown-linux-musl.tgz \
    | tar -xzf - -C /usr/local/cargo/bin cargo-binstall
RUN cargo binstall cargo-leptos --locked -y
RUN cargo binstall wasm-opt --locked -y
