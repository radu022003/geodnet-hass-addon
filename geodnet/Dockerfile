ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:7.3.1

# ARGS...

FROM ${BUILD_FROM} AS base

ENV DEBIAN_FRONTEND "noninteractive"

RUN mv /init /s6init
FROM base AS builder
ARG BUILD_ARCH



# Clone application repository
RUN git clone https://github.com/erikarenhill/geodnet-headless-console-api

# Copy app source
WORKDIR /geodnet-headless-console-api

# Install app dependencies
RUN npm ci

# Expose port
EXPOSE 3000

# Start the app
CMD ["node", "index.js"]