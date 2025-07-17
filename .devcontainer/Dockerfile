FROM mcr.microsoft.com/devcontainers/rust:latest

USER root
RUN apt-get update && apt-get install -y musl-tools
RUN apt-get update && apt-get install -y chromium
RUN apt-get update && apt-get install -y fonts-ipafont-gothic fonts-ipafont-mincho
# RUN apt-get update && apt-get install -y pandoc

USER vscode
RUN cargo install cargo-binstall --features rustls --locked
RUN cargo binstall taplo-cli
RUN cargo binstall cargo-leptos --locked
