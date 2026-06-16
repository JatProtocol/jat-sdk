## Summary

What this change does in the SDK or a service.

## Surfaces

- [ ] `packages/seal-sdk` and `sdk/` reference impl kept in step
- [ ] Wire format unchanged, or updated to match `jat-program` / `jat-circuits` (link PRs)

## Privacy and safety

- [ ] Keys stay in the caller's process; nothing secret is logged or sent
- [ ] Relayer stays un-drainable; new accept/reject paths covered in `relay.test.mjs`
- [ ] Indexer still serves only public data

## Testing

- [ ] `npm test` passes
- [ ] `npx tsc --noEmit` passes for `packages/seal-sdk`
- [ ] Relevant `e2e_*.mjs` run against devnet if the flow changed
