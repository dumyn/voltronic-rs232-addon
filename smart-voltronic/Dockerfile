
ARG BUILD_FROM=ghcr.io/hassio-addons/base:21.0.7
FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Actualizar los índices e instalar las dependencias
# en una sola operación para reducir conflictos.
RUN apk update && \
    apk upgrade --available --no-cache && \
    apk add --no-cache \
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
RUN python3 --version && \
    node --version && \
    npm --version

# Instalar Node-RED.
RUN npm install -g --no-audit --no-fund node-red@5.0.7 && \
    npm cache clean --force

# Copiar los archivos del complemento.
COPY . /addon
WORKDIR /addon

# Instalar la dependencia WebSocket.
RUN npm init -y >/dev/null 2>&1 || true
RUN npm install --no-audit --no-fund ws
RUN chmod a+x /addon/run.sh

ENTRYPOINT ["/addon/run.sh"]

