ARG UBUNTU_VERSION
FROM ubuntu:${UBUNTU_VERSION}

# update ca-certificates
RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
    && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# timezone
RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        tzdata \
    && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* \
    && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && echo 'Asia/Tokyo' >/etc/timezone

# language-pack
RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        language-pack-ja-base \
        language-pack-ja \
    && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
ENV LANG=ja_JP.UTF-8

# vscode user
RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        sudo \
    && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* \
    && echo "vscode ALL=(ALL) NOPASSWD:ALL" >>/etc/sudoers.d/ALL \
    && groupadd \
        --gid 5000 \
        vscode \
    && useradd \
        --uid 5000 \
        --gid 5000 \
        --home-dir /home/vscode \
        --create-home \
        --shell /bin/bash \
        vscode

# common dev tools
RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        bash-completion \
        curl \
        git \
        gnupg2 \
        iputils-ping \
        less \
        net-tools \
        tar \
        time \
        unzip \
        xz-utils \
        zip \
    && apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

USER vscode

# rust
ARG RUST_VERSION
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain=${RUST_VERSION}
