FROM jetpackio/devbox:0.16.0 AS builder

WORKDIR /code/vscode-base
USER root:root
RUN mkdir -p /code/vscode-base && chown ${DEVBOX_USER}:${DEVBOX_USER} /code/vscode-base
USER ${DEVBOX_USER}:${DEVBOX_USER}

COPY --chown=${DEVBOX_USER}:${DEVBOX_USER} devbox.json devbox.json
COPY --chown=${DEVBOX_USER}:${DEVBOX_USER} devbox.lock devbox.lock
RUN devbox install


FROM aazw/devcontainers-devbox-go:7 AS runtime

USER root
COPY --from=builder /nix/store /nix/store
COPY --from=builder /code/vscode-base/.devbox /code/vscode-base/.devbox
USER vscode

ENV PATH="/code/vscode-base/.devbox/nix/profile/default/bin:${PATH}"



