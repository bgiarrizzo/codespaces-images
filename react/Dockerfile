ARG VARIANT="20"
FROM mcr.microsoft.com/devcontainers/typescript-node:1-${VARIANT}

EXPOSE 3000
ARG NODE_MODULES="tslint-to-eslint-config typescript next react react-dom"

# Update APT Cache
RUN apt update

# Purge Non Secure Packages
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get purge -y imagemagick imagemagick-6-common 

# Configure Base System
RUN mkdir -p /workspaces/app/

# Configure Base React
RUN su node -c "umask 0002 && npm install -g ${NODE_MODULES}"

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pip-tmp \
    && npm cache clean --force > /dev/null 2>&1

WORKDIR /workspaces/app/
