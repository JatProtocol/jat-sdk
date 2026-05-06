# Runs a SEAL service (relayer or indexer). Build from the repo root:
#   docker build -f ops/Dockerfile -t seal-svc .
# The relayer keypair is a SECRET: never bake it into the image. Mount it at
# runtime (see ops/docker-compose.yml) and point RELAYER_WALLET at the mount.
FROM node:20-slim
WORKDIR /app

# install only what the services need (web3.js + circomlibjs for pool reconstruction)
COPY package.json ./
RUN npm install --omit=dev --no-audit --no-fund \
  && npm install @solana/web3.js@^1.98.4 circomlibjs@^0.1.7 --no-audit --no-fund

COPY sdk ./sdk

ENV RPC_URL=https://api.devnet.solana.com
# SERVICE = relayer | indexer
ENV SERVICE=relayer
EXPOSE 8789 8788
CMD ["sh", "-c", "node sdk/${SERVICE}.mjs"]
