FROM rust-base:latest
ARG DEVS_GROUPNAME="devs"
ARG BUILDER_USERNAME="builder"
ARG DEV_USER_USERNAME="dev-user"
ARG DEV_USER_UID="1000"

USER root

# zsh インストール
RUN apt-get update && apt-get install zsh -y

# dev-user ユーザー作成
RUN useradd --create-home --uid ${DEV_USER_UID} --shell /bin/zsh ${DEV_USER_USERNAME} &&\
    usermod --append --groups ${DEVS_GROUPNAME} ${DEV_USER_USERNAME}

USER ${BUILDER_USERNAME}
RUN cargo binstall stylance-cli --locked -y
RUN cargo binstall mdbook mdbook-mermaid mdbook-pdf mdbook-pandoc --locked -y

USER ${DEV_USER_USERNAME}
