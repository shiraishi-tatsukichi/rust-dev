FROM rust-base:latest
ARG BUILDER_USERNAME="builder"
ARG BUILDER_GROUPNAME=${BUILDER_USERNAME}
ARG DEV_USER_USERNAME="dev-user"
ARG DEV_USER_UID="1000"

USER root

# zsh インストール
RUN apt-get update && apt-get install zsh -y

RUN apt-get update && apt-get install pandoc -y

# dev-user ユーザー作成
RUN useradd --create-home --uid ${DEV_USER_UID} --shell /bin/zsh ${DEV_USER_USERNAME} &&\
    usermod --append --groups ${BUILDER_GROUPNAME} ${DEV_USER_USERNAME}

USER ${BUILDER_USERNAME}
RUN cargo install stylance-cli
RUN cargo install mdbook
RUN cargo install mdbook-mermaid
RUN cargo install mdbook-metadata
RUN cargo install mdbook-pandoc
RUN cargo install mdbook-codename
RUN cargo install mdbook-pdf --features fetch

RUN chmod g+rw -R /usr/local/cargo/registry

USER ${DEV_USER_USERNAME}
