ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:7.3.1

FROM ${BUILD_FROM} AS base
# Prevent dpkg errors
ENV DEBIAN_FRONTEND=noninteractive
# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Install dependencies for Puppeteer


# Add Google Chrome repository
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

# Install Google Chrome
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /var/cache/apt/* /var/cache/apt/archives/*

RUN apt-get update && apt-get install -y npm nodejs && apt-get clean

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