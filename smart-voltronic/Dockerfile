ARG BUILD_FROM=ghcr.io/hassio-addons/base:latest
FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Instalar dependencias necesarias.
RUN apk add --no-cache \
    bash \
    jq \
    tzdata \
    python3 \
    make \
    g++ \
    linux-headers \
    nodejs \
    npm

# Comprobar las versiones instaladas.
RUN node --version && npm --version

# Instalar Node-RED.
RUN npm install -g --no-audit --no-fund node-red@5.0.7 \
    && npm cache clean --force

# Copiar la aplicación.
COPY . /addon
WORKDIR /addon

# Instalar las dependencias.
RUN npm init -y >/dev/null 2>&1 || true \
    && npm install --no-audit --no-fund ws \
    && chmod a+x /addon/run.sh

ENTRYPOINT ["/addon/run.sh"]
