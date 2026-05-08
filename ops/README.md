# Hosting the SEAL services

Two stateless Node services back the product:

- **relayer** (`:8789`) pays user fees so a fresh stealth account never originates
  one. It holds a funded keypair and is hardened against drain (see `SECURITY.md`):
  program allowlist, no relayer-funded System instructions, a simulated per-tx
  cost cap, a balance floor, and per-IP / global rate limits.
- **indexer** (`:8788`) serves public data only (`/announcements`, `/pool/leaves`).
  It never sees a scan key; clients rebuild their own Merkle paths.

## Run

```bash
# fund a fresh keypair for the relayer and save it OUTSIDE the repo, then:
export RELAYER_WALLET_FILE=/secure/path/relayer-wallet.json
export RPC_URL=https://your-rpc          # a dedicated RPC is strongly recommended
docker compose -f ops/docker-compose.yml up --build -d
```

Point the SDK / web app at them:

```
NEXT_PUBLIC_RELAYER_URL=https://relayer.yourdomain
NEXT_PUBLIC_INDEXER_URL=https://indexer.yourdomain
```

## Operational notes

- **Use a dedicated RPC.** Public RPC rate-limits `getProgramAccounts` and
  `getTransaction`, which the indexer relies on; the throttle/retry built in helps
  but is not a substitute.
- **Keep the relayer funded.** It refuses to relay below `RELAYER_MIN_BALANCE_LAMPORTS`.
  Each relay costs at most `MAX_RELAYER_COST_LAMPORTS` (fee + a small protocol rent).
- **The keypair is a secret.** It is mounted via a Docker secret, never baked into
  the image or committed. Rotate it if exposed.
- **Put a reverse proxy / WAF in front** for TLS and as a second rate-limit layer.
