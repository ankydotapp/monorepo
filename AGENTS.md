# AGENTS.md

This file defines how AI agents should work inside the Anky monorepo.

It applies to Codex, Claude, Hermes, Anky, and any other coding or operating agent with access to this repository.

## 1. First Read

Before making meaningful changes, read:

```txt
docs/MASTER_REGISTRY.md
docs/ANKY_TREASURY_SETUP.md
docs/BANKR_LAUNCH_RUNBOOK.md
```

`docs/MASTER_REGISTRY.md` is the operational source of truth.

If anything conflicts with it, the registry wins.

## 2. Repo Identity

Canonical repo:

```txt
github.com/ankydotapp/monorepo
```

Do not refer to `anky-seed` as the master repo unless discussing history.

## 3. Core Product Invariants

Do not break these:

```txt
Anky is an 8-minute writing app.
Writing is forward-only.
Backspace is disabled.
Paste is disabled.
Newline is disabled.
8 seconds of silence closes the session.
.anky is the protocol artifact.
Raw writing should not become a stored server asset.
The app does not require the token.
```

Any change that violates these requires explicit human approval.

## 4. Money / Treasury Rules

The intended canonical flow is:

```txt
Bankr trading fees
→ Splits Treasury
→ accounting/export/offramp
→ Mercury
```

Canonical onchain business layer:

```txt
Splits Treasury
```

Canonical fiat account:

```txt
Mercury / Anky, Inc.
```

Intended Bankr fee beneficiary:

```txt
ANKY_BANKR_FEES
```

Do not change treasury addresses, fee beneficiaries, token deployment settings, signer thresholds, Bankr settings, Splits settings, or Mercury-related assumptions without explicit human confirmation.

Any update to a canonical financial value must also update:

```txt
docs/MASTER_REGISTRY.md
```

## 5. Agent Signing Rules

Anky / Hermes may be a signer.

Anky / Hermes must never use JP’s private key, seed phrase, passkey, personal wallet, or personal credentials.

The agent must have its own key.

Secrets must be stored outside the repo.

Never commit:

```txt
.env
API keys
private keys
seed phrases
wallet JSON files
Bankr keys
Splits keys
Mercury credentials
RevenueCat keys
App Store credentials
Google Play credentials
```

## 6. Bankr / Token Rules

The Bankr/Base `$ANKY` deployment is not canonical until these are recorded in `docs/MASTER_REGISTRY.md`:

```txt
contract address
deployment transaction
fee beneficiary
deployer
chain
token image
website
launch date
```

The Solana `$ANKY` token is historical/genesis unless the registry says otherwise.

Do not use public language that implies:

```txt
investment
profit promise
holder revenue share
guaranteed upside
dividends
passive income
```

Safe language:

```txt
The token serves the ritual.
The app does not require the token.
Fees fund compute, art, infrastructure, operations, and public expansion.
```

## 7. Code Change Rules

Prefer small changes.

Preserve existing architecture.

Do not introduce new frameworks, package managers, databases, queues, cloud providers, or auth systems unless explicitly asked.

Before editing:

```bash
pwd
ls
find . -maxdepth 2 -type f | sort | head -200
```

Before adding commands, inspect:

```bash
package.json
bunfig.toml
tsconfig.json
```

Run only scripts that exist.

Prefer:

```bash
bun run lint
bun run typecheck
bun test
```

if those commands are present.

## 8. Documentation Rules

When changing canonical reality, update the registry.

Canonical reality includes:

```txt
company identity
repo identity
domains
emails
bundle IDs
package IDs
treasury accounts
wallets
token addresses
Bankr fee beneficiary
Splits subaccounts
agent signers
production endpoints
app review language
covenant URLs
```

Documentation should be direct and boring.

No vague language around operational facts.

## 9. App Review Language

Use boring app review language:

```txt
Anky is an 8-minute private writing app.

Users write continuously during a timed session.
The app stores writing locally on device.
After a session, users may optionally request a reflection.
No account is required.
Test credentials are not needed.
```

Do not mention token mechanics in app review notes unless required.

## 10. Privacy Rules

Do not add logging of raw writing.

Do not log private user text.

Do not store raw `.anky` content on the server unless explicitly approved.

Do not send writing to third-party services except through the approved reflection path.

Logs should avoid:

```txt
raw writing
full prompts
private keys
signatures
trial proofs
account secrets
payment credentials
```

## 11. Deployment Rules

Never deploy production without explicit instruction.

Never launch or redeploy a token without explicit instruction.

Never change a fee recipient without explicit instruction.

Never run a treasury transaction without explicit instruction.

Before any production operation, summarize:

```txt
what will happen
which account/wallet is involved
which chain/environment is involved
what the irreversible consequence is
how to verify success
```

Then wait for confirmation.

## 12. Failure Rules

If something goes wrong:

```txt
stop
record facts
do not hide history
do not make emotional public claims
do not redeploy reflexively
ask for confirmation before correction
```

For token, treasury, or production incidents, update `docs/MASTER_REGISTRY.md` only after the correction is real and verified.

## 13. Style

Write code that is boring, readable, and maintainable.

Write docs that are precise.

Use the smallest useful abstraction.

Prefer explicit names over clever names.

Do not overbuild.

## 14. Final Law

The ritual comes first.

The token serves the ritual.

The agent can act.

The company keeps records.

The registry wins.
