---
name: Bug report
about: A scan that misses a payment, a claim or withdraw that fails, or a relayer that rejects a valid tx
title: "[bug] "
labels: bug
---

## What happened

Describe the incorrect behavior in the SDK or a service.

## What you expected

What should have happened instead.

## Reproduction

- Surface: packages/seal-sdk or sdk/ reference impl
- Flow: pay / scanOnChain / claimToAddress / claimIntoPool / withdraw
- Service: relayer / indexer (and the response or error it returned)
- Node version, RPC, and whether you were on devnet

## Cross-repo

- Did a wire-format change land in `jat-program` or `jat-circuits` without a matching SDK
  change? `sdk/contract.test.mjs` pins the discriminators against the IDL.
