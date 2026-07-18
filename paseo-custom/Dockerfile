FROM ghcr.io/getpaseo/paseo:latest

ARG USERNAME=paseo

USER root

RUN apt-get update && apt-get install -y \
    sudo \
    && rm -rf /var/lib/apt/lists/*

RUN echo '#!/bin/sh\n\
if [ "$PASEO_SUDO_ENABLED" = "true" ]; then\n\
    echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/paseo-relay\n\
else\n\
    rm -f /etc/sudoers.d/paseo-relay\n\
    echo "Sudo non abilitato (PASEO_SUDO_ENABLED non è true)"\n\
fi\n\
exec runuser -u '${USERNAME}' -- "$@"' > /usr/local/bin/entrypoint.sh \
    && chmod +x /usr/local/bin/entrypoint.sh

RUN npm install -g @anthropic-ai/claude-code \
    && npm install -g @openai/codex \
    && npm install -g opencode-ai \
    && npm install -g --ignore-scripts @earendil-works/pi-coding-agent

USER root

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
