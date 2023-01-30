# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG VARIANT=18-bullseye
FROM mcr.microsoft.com/devcontainers/typescript-node:${VARIANT}

EXPOSE 3000

# Install Repo for Github CLI
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# Install fontconfig + Hack Nerd Font
RUN wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.2.2/Hack.zip \
    && mkdir -p /workspaces/app/ \
    && apt update && apt-get -y install --no-install-recommends fontconfig bat exa gh \
    && ln -s /usr/bin/batcat /usr/bin/bat \
    && unzip Hack.zip -d /usr/share/fonts/truetype \
    && fc-cache -f -v

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pip-tmp

RUN su node -c "umask 0002 && npm install -g next react react-dom"

WORKDIR /workspaces/app/

