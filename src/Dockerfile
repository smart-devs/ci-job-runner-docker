ARG FROM=""
# hadolint ignore=DL3007,DL3006
FROM ${FROM}
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /tmp/

ENV DOCKER_HOST "tcp://localhost:2375"

ARG DOCKER_VERSION="18.06.1~ce~3-0~debian"

ARG CONTAINER_RUNTIME_REQUIREMENTS=""
ARG CONTAINER_EXTRA_RUNTIME_REQUIREMENTS=""
ARG CONTAINER_BUILD_REQUIREMENTS="curl gnupg apt-transport-https software-properties-common"
ARG CONTAINER_EXTRA_BUILD_REQUIREMENTS=""

ARG DOCKER_AUTH_CONFIG=""

COPY FS/ /

# hadolint ignore=DL4006,DL3008,SC2086
RUN set -Eeu; \
    /usr/local/bin/install-container-requirements; \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 0; \
    mkdir -p ~/.docker; \
    echo "${DOCKER_AUTH_CONFIG}" > ~/.docker/config.json; \
    curl -fsSL https://download.docker.com/linux/debian/gpg  | apt-key add -; \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable"; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends docker-ce=${DOCKER_VERSION}; \
    curl -s -L -o /usr/local/bin/docker-credential-ecr-login https://s3.eu-central-1.amazonaws.com/valmano-gitlab-helper/docker-credential-ecr-login; \
    chown root:root /usr/local/bin/docker-credential-ecr-login; \
    chmod -R 755 /usr/local/bin/*; \
    /usr/local/bin/docker-image-clean
