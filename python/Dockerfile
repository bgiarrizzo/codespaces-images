ARG VARIANT="3"
FROM python:${VARIANT}

ENV PYTHONUNBUFFERED 1
ARG NODE_VERSION="lts/*"

# Update APT Cache
RUN apt update

# Purge Non Secure Packages
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get purge -y imagemagick imagemagick-6-common 

# Configure Base System
RUN mkdir -p /workspaces/app/

# Configure Base Python
RUN python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pip \
    && python -m pip --disable-pip-version-check --no-cache-dir install --upgrade pipenv \
    && python -m pip install --upgrade setuptools 

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pip-tmp
