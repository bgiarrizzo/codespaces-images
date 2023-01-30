# Variant versions availables : https://mcr.microsoft.com/v2/vscode/devcontainers/python/tags/list
ARG VARIANT=3-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/python:${VARIANT}

ENV PYTHONUNBUFFERED 1

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="lts/*"

# Install Repo for Github CLI
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

RUN mkdir -p /workspaces/app/ \
    && apt update && apt-get -y install --no-install-recommends bat exa gh \
    && ln -s /usr/bin/batcat /usr/bin/bat

# Configure Base System
RUN python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pip \
    && python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pipenv

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pip-tmp

USER vscode 
RUN mkdir -p /home/vscode/.config/gh/ \
    && mkdir -p /home/vscode/.config/vscode-dev-containers/