# Secrets Management Reference

A secret is any credential that grants access or proves identity: an API key, a password, a token, a private key, a database connection string. Managing secrets means keeping them out of places they can leak, code, public repositories, frontend bundles, logs, screenshots, storing them where access is controlled, scoping each one to the least it needs, rotating them on a schedule, and treating any secret that ever touched a public place as compromised. A leaked secret is an open door, and most leaks are avoidable.

## What is inside

- [01-what-counts-as-a-secret.md](01-what-counts-as-a-secret.md) recognizing what needs protecting
- [02-keep-secrets-out-of-code.md](02-keep-secrets-out-of-code.md) the places secrets must never go
- [03-environment-variables-and-vaults.md](03-environment-variables-and-vaults.md) where secrets should live instead
- [04-rotation-and-least-privilege.md](04-rotation-and-least-privilege.md) limiting the blast radius of any one secret
- [05-what-to-do-when-one-leaks.md](05-what-to-do-when-one-leaks.md) responding when a secret is exposed

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright (c) 2026 0xelitesystem.
