# Variant versions availables : https://mcr.microsoft.com/v2/vscode/devcontainers/python/tags/list
ARG VARIANT=3-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/python:${VARIANT}

ENV PYTHONUNBUFFERED 1

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="lts/*"

# Install fontconfig + Hack Nerd Font
RUN apt-get update \
    && mkdir /workspaces/app/ \
    && apt-get -y install --no-install-recommends fontconfig bat exa \
    && wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.2.2/Hack.zip \
    && unzip Hack.zip -d /usr/share/fonts/truetype \
    && fc-cache -f -v

# Configure Base System
RUN python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pip \
    && python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pipenv

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pip-tmp
