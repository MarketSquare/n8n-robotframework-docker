ARG NODE_VERSION

FROM delilovic/n8n_base:${NODE_VERSION}-bookworm-slim

ARG N8N_VERSION
ARG N8N_RELEASE_TYPE=dev
ARG IMAGE_DESCRIPTION="Workflow Automation Tool"
ENV NODE_ENV=production
ENV N8N_RELEASE_TYPE=${N8N_RELEASE_TYPE}
ENV SHELL=/bin/sh
# Restrict GraphicsMagick to its commonly used coder set.
ENV MAGICK_CODER_STABILITY=PRIMARY

WORKDIR /home/node

COPY docker/images/n8n/docker-entrypoint.sh /

RUN set -e; \
    npm install -g n8n@${N8N_VERSION}; \
    mkdir -p /home/node/.n8n; \
    chown -R node:node /home/node; \
    rm -rf /root/.npm /tmp/*

EXPOSE 5678/tcp
USER node
ENTRYPOINT ["tini", "--", "/docker-entrypoint.sh"]

LABEL org.opencontainers.image.title="n8n" \
      org.opencontainers.image.description="${IMAGE_DESCRIPTION}" \
      org.opencontainers.image.source="https://github.com/n8n-io/n8n" \
      org.opencontainers.image.url="https://n8n.io" \
      org.opencontainers.image.version=${N8N_VERSION}
