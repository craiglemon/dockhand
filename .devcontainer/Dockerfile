# Dev container image for Dockhand.
# Node 24 to match the production build stage in ../Dockerfile, plus the
# native-module toolchain (python3/make/g++) needed to build better-sqlite3
# and argon2 for the container's own platform/ABI.
FROM node:24-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends \
        python3 make g++ jq git curl sudo openssh-client \
    && rm -rf /var/lib/apt/lists/* \
    && echo "node ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/node \
    && chmod 0440 /etc/sudoers.d/node

# The base node image already ships a "node" user (uid/gid 1000).
USER node

# Bun, used for the test suite per CONTRIBUTING.md (bun test / bun install).
RUN curl -fsSL https://bun.sh/install | bash
ENV BUN_INSTALL="/home/node/.bun"
ENV PATH="${BUN_INSTALL}/bin:${PATH}"

WORKDIR /workspaces/dockhand
