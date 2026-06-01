# Bankr Launch Runbook

This document defines the launch procedure for the canonical Bankr/Base deployment of `$ANKY`.

The goal is not just to launch a token.

The goal is to give Anky a clean economic body.

## 1. Launch Principle

The canonical `$ANKY` token should be deployed by Anky / Hermes through Bankr.

JP acts as steward/operator of Anky, Inc.

Anky acts as the agent deployer.

Fees flow to the company’s onchain business layer.

```txt
Anky deploys.
Splits receives.
Mercury settles fiat.
The registry records truth.
```

## 2. Canonical Token Fields

| Field                  | Value                                        |
| ---------------------- | -------------------------------------------- |
| Name                   | Anky                                         |
| Symbol                 | ANKY                                         |
| Chain                  | Base                                         |
| Deployment method      | Bankr                                        |
| Deployer               | Anky / Hermes agent                          |
| Fee beneficiary        | `ANKY_BANKR_FEES` Splits Treasury subaccount |
| Website                | `https://anky.app`                           |
| Token image            | TBD                                          |
| Dexscreener art        | TBD                                          |
| Covenant v2            | TBD                                          |
| Contract address       | TBD                                          |
| Deployment transaction | TBD                                          |
| Pool address           | TBD                                          |
| Bankr profile          | TBD                                          |

## 3. Historical Token

The Solana `$ANKY` token is the genesis token.

```txt
Chain: Solana
Address: 6GsRbp2Bz9QZsoAEmUSGgTpTW7s59m7R3EGtm1FPpump
Status: Historical / genesis
```

Launch language should not frame the Base deployment as shame, quitting, or deletion.

Use:

```txt
The Solana token was the spark.
The Bankr/Base token is the operating body.
```

## 4. Fee Destination

The required invariant before launch:

```txt
BANKR_FEE_BENEFICIARY=ANKY_BANKR_FEES_ADDRESS
```

Do not deploy until this is true.

Do not use a temporary wallet.

Do not use JP’s personal wallet.

Do not use the loose Bankr agent wallet unless Bankr/Splits makes direct fee routing impossible.

If direct routing is impossible, document the fallback clearly:

```txt
Bankr fee beneficiary = Anky Bankr wallet
Required sweep = Anky Bankr wallet → ANKY_BANKR_FEES
Sweep cadence = immediate / daily / weekly
Reason = direct Splits fee beneficiary unsupported
```

## 5. Preflight Checklist

### Treasury

```txt
[ ] Splits Team exists for Anky, Inc.
[ ] ANKY_BANKR_FEES subaccount exists.
[ ] Signers are JP / Brother / Anky-Hermes.
[ ] Threshold is 2-of-3.
[ ] Test inbound transfer completed.
[ ] Test 2-of-3 transaction completed.
[ ] Export/reporting test completed.
[ ] ANKY_BANKR_FEES_ADDRESS recorded in MASTER_REGISTRY.md.
```

### Bankr

```txt
[ ] Dedicated Anky / Hermes Bankr account exists.
[ ] Bankr API key is stored outside the repo.
[ ] Bankr API key is not in git history.
[ ] Bankr wallet security limits reviewed.
[ ] Bankr wallet balance checked.
[ ] Bankr account can deploy on Base.
[ ] Bankr can route fees to an explicit fee beneficiary.
[ ] Fee beneficiary address verified character by character.
```

### Art / Metadata

```txt
[ ] Token image final.
[ ] Dexscreener art final.
[ ] Website ready at anky.app.
[ ] App download link ready or acceptable temporary landing page ready.
[ ] Covenant v2 drafted.
[ ] Launch post drafted.
[ ] Token description drafted.
[ ] Public explanation of Solana genesis token drafted.
```

### Legal / Comms Hygiene

```txt
[ ] No promise of profit.
[ ] No holder revenue share language.
[ ] No dividend language.
[ ] No guaranteed upside language.
[ ] No claim that token is required to use the app.
[ ] No claim that buying token gives ownership of Anky, Inc.
[ ] Fees described as funding compute, infrastructure, art, operations, and public expansion.
```

## 6. Token Description

Use this as the default description:

```txt
Anky is an 8-minute writing app.

You write forward.
No backspace.
No performance.
No audience required.

Anky witnesses the ritual.

$ANKY exists to expand the Anky meme and fund Anky’s compute, art, infrastructure, and public operations.
```

Short version:

```txt
Anky is an 8-minute writing ritual. $ANKY funds the agent, the app, and the public expansion of the meme.
```

## 7. Bankr Deployment Prompt

Before running this, replace every placeholder.

```txt
Deploy a token on Base through Bankr.

Name: Anky
Symbol: ANKY
Website: https://anky.app
Image: <TOKEN_IMAGE_URL>
Description: Anky is an 8-minute writing app. You write forward. No backspace. No performance. No audience required. Anky witnesses the ritual. $ANKY exists to expand the Anky meme and fund Anky’s compute, art, infrastructure, and public operations.
Fee beneficiary: <ANKY_BANKR_FEES_ADDRESS>
```

After generating the Bankr command or transaction, stop and verify:

```txt
[ ] Chain is Base.
[ ] Name is Anky.
[ ] Symbol is ANKY.
[ ] Fee beneficiary is ANKY_BANKR_FEES_ADDRESS.
[ ] Website is anky.app.
[ ] Image URL is final.
[ ] Description has no investment language.
```

Only then execute.

## 8. Execution Procedure

### Step 1 — Confirm current registry

Open:

```txt
docs/MASTER_REGISTRY.md
docs/ANKY_TREASURY_SETUP.md
docs/BANKR_LAUNCH_RUNBOOK.md
```

Confirm there are no `TBD` values blocking deployment.

### Step 2 — Confirm Bankr identity

Run the Bankr equivalent of:

```bash
bankr whoami
bankr wallet portfolio --chain base
```

Confirm this is the Anky / Hermes agent account, not JP’s personal account.

### Step 3 — Confirm Splits fee beneficiary

Confirm:

```txt
ANKY_BANKR_FEES_ADDRESS=
```

Then compare the address in:

```txt
MASTER_REGISTRY.md
Splits dashboard
Bankr deployment prompt
```

They must match.

### Step 4 — Deploy

Have Anky / Hermes deploy through Bankr.

Save the raw command/prompt used.

Save the response.

### Step 5 — Record outputs

Immediately record:

```txt
ANKY_BASE_TOKEN_ADDRESS=
BANKR_DEPLOYMENT_TX=
POOL_ADDRESS=
BANKR_DEPLOYER_ADDRESS=
BANKR_FEE_BENEFICIARY=
TOKEN_IMAGE_URL=
DEXSCREENER_URL=
BANKR_PROFILE_URL=
```

### Step 6 — Verify onchain

Confirm:

```txt
[ ] Token exists on Base.
[ ] Token name is Anky.
[ ] Token symbol is ANKY.
[ ] Deployer is the intended Bankr/Anky flow.
[ ] Fee beneficiary is ANKY_BANKR_FEES_ADDRESS.
[ ] Liquidity/pool exists.
[ ] Website and image metadata resolve.
```

### Step 7 — Update files

Update:

```txt
docs/MASTER_REGISTRY.md
docs/ANKY_TREASURY_SETUP.md
docs/BANKR_LAUNCH_RUNBOOK.md
```

Commit:

```bash
git add docs/MASTER_REGISTRY.md docs/ANKY_TREASURY_SETUP.md docs/BANKR_LAUNCH_RUNBOOK.md
git commit -m "Define canonical Anky treasury and Bankr launch"
```

After deployment:

```bash
git add docs/MASTER_REGISTRY.md docs/BANKR_LAUNCH_RUNBOOK.md
git commit -m "Record canonical ANKY Base deployment"
```

## 9. Post-Launch Checklist

Within the first hour:

```txt
[ ] Update MASTER_REGISTRY with contract address.
[ ] Update website with canonical token address.
[ ] Publish covenant v2 or mark covenant v2 pending.
[ ] Update Dexscreener metadata/art if available.
[ ] Verify fee beneficiary once more.
[ ] Archive screenshots/receipts.
[ ] Save deployment prompt and response.
```

Within the first day:

```txt
[ ] Test fee claim path if fees exist.
[ ] Confirm claimed assets arrive in the expected place.
[ ] Confirm Splits export captures the event.
[ ] Add accounting memo: BANKR_TRADING_FEE_REVENUE.
[ ] Create first monthly reconciliation folder.
```

Within the first week:

```txt
[ ] Decide whether to automate swaps.
[ ] Decide whether to create ANKY_TAX_RESERVE.
[ ] Decide whether to create ANKY_AGENT_OPS.
[ ] Review language with CPA/legal counsel.
[ ] Update covenant v2 with final token details.
```

## 10. Public Launch Post Draft

```txt
Anky has a new economic body.

The Solana $ANKY was the spark.
The Bankr/Base $ANKY is the operating body.

It was deployed by Anky, the agent.
Fees flow into the Anky, Inc. onchain treasury through Splits.

The app remains simple:
write for 8 minutes.
no backspace.
no performance.
no audience required.

The token does not replace the ritual.
The token serves the ritual.

anky.app
```

## 11. Solana-to-Base Explanation

Use this when people ask why there are two tokens:

```txt
The Solana token was the genesis spark of $ANKY.

As Anky became a real company, app, and agent, we needed a cleaner operating structure from day 0: agent deployment, fee routing, treasury records, accounting exports, and a direct path into Anky, Inc.

The Bankr/Base deployment is the canonical economic container going forward.

The app does not require the token.
The token exists to expand the meme and fund the work.
```

## 12. Do Not Say

Avoid:

```txt
migration guarantees value
holders will be rewarded
buy before announcement
fees go to holders
revenue share
investment opportunity
passive income
guaranteed upside
official compensation for v1 holders
```

Use:

```txt
genesis token
historical token
canonical economic container
fees fund operations
agent-deployed
company treasury
onchain records
```

## 13. Failure / Confusion Procedure

If anything is wrong after deployment:

```txt
Do not immediately redeploy.
Do not delete history.
Do not make emotional public claims.
Freeze the registry.
Write the facts.
Ask Bankr/Splits for the cleanest correction.
Publish only what is verified.
```

If the fee beneficiary is wrong:

```txt
Document the mistake.
Determine whether Bankr allows fee beneficiary transfer.
Do not claim the wrong path is canonical.
Update MASTER_REGISTRY only after the correction is executed.
```

## 14. Final Law

The token serves the ritual.

The agent can act.

The company keeps records.

The registry wins.
