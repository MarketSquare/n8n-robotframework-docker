ARG N8N_VERSION

FROM delilovic/n8n:${N8N_VERSION}-bookworm-slim

ARG ROBOTFRAMEWORK_VERSION
ARG RF_BROWSER_VERSION
ARG RF_ASSERTION_ENGINE_VERSION
ARG RF_JSONLIBRARY_VERSION

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 python3-pip curl && \
    pip3 install --no-cache-dir --break-system-packages \
        robotframework==${ROBOTFRAMEWORK_VERSION} \
        robotframework-browser==${RF_BROWSER_VERSION} \
        robotframework-assertion-engine==${RF_ASSERTION_ENGINE_VERSION} \
        robotframework-jsonlibrary==${RF_JSONLIBRARY_VERSION} && \
    npx playwright install-deps && \
    rfbrowser init

USER node
