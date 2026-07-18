FROM ghcr.io/getpaseo/paseo:latest

ARG USERNAME=paseo

USER root

RUN apt-get update && apt-get install -y \
    sudo \
    && rm -rf /var/lib/apt/lists/*

RUN echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN npm install -g @anthropic-ai/claude-code \
    && npm install -g @openai/codex \
    && npm install -g opencode-ai \
    && npm install -g --ignore-scripts @earendil-works/pi-coding-agent

USER ${USERNAME}

