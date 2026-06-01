# Anky Monorepo

Anky is an 8-minute writing app.

You write forward.
No backspace.
No paste.
No newline.
No performance.
No audience required.

Anky witnesses the ritual.

This repository is the canonical monorepo for Anky.

## Canonical Source of Truth

The operational source of truth is:

```txt
docs/MASTER_REGISTRY.md
```

If another file, dashboard, memory, README, branch, covenant, token page, app build, wallet note, or social post conflicts with `docs/MASTER_REGISTRY.md`, the registry wins until intentionally updated.

## Core Product Law

Anky’s core ritual is simple:

```txt
write for 8 minutes
write forward only
no backspace
no paste
no newline
8 seconds of silence closes the session
```

The protocol artifact is:

```txt
.anky
```

The reflection endpoint is:

```txt
POST /anky
```

The privacy invariant is:

```txt
Raw writing should not become a stored server asset.
```

## Canonical Stack

| Layer                   | Canonical                        |
| ----------------------- | -------------------------------- |
| Company                 | Anky, Inc.                       |
| Repo                    | `github.com/ankydotapp/monorepo` |
| Domain                  | `anky.app`                       |
| Support                 | `support@anky.app`               |
| Founder/admin           | `jp@anky.app`                    |
| Android package         | `app.anky.mobile`                |
| iOS bundle              | `com.jpfraneto.Anky`             |
| Fiat account            | Mercury                          |
| Onchain business layer  | Splits Treasury                  |
| Token deployment engine | Bankr                            |
| Agent/operator          | Anky / Hermes                    |
| Protocol                | `.anky`                          |

## Important Documents

```txt
docs/MASTER_REGISTRY.md
docs/ANKY_TREASURY_SETUP.md
docs/BANKR_LAUNCH_RUNBOOK.md
```

Read these before changing anything related to:

* company identity
* app identity
* treasury
* token deployment
* Bankr
* Splits
* wallets
* public support emails
* covenant
* app review notes
* production infrastructure

## Economic Layer

The app does not require the token.

The token serves the ritual.

The intended canonical economic flow is:

```txt
Bankr trading fees
→ Splits Treasury
→ accounting/export/offramp
→ Mercury
```

The Solana `$ANKY` token is historical/genesis.

The intended canonical economic container is the Bankr/Base `$ANKY` token once deployed and recorded in `docs/MASTER_REGISTRY.md`.

Do not use investment language.

Do not describe `$ANKY` as:

```txt
investment
returns
dividends
revenue share
guaranteed upside
passive income
holder earnings
```

Use:

```txt
$ANKY exists to expand the Anky meme and fund Anky’s compute, art, infrastructure, and public operations.
```

## Development

Before making changes, inspect the repo structure and existing package manager.

Do not invent new architecture unless explicitly asked.

Prefer small, reversible changes.

When possible, run the existing checks before committing:

```bash
# inspect available scripts first
cat package.json
```

Then run the appropriate existing commands, such as:

```bash
bun test
bun run lint
bun run typecheck
```

Only run commands that exist in the repo.

## Deployment

Never deploy production changes, tokens, treasury actions, or app store builds without explicit human confirmation.

Never use temporary wallets or personal wallets for canonical company flows.

Never commit secrets.

## Final Law

The myth can be weird.

The money flow must be boring.

The registry wins.
