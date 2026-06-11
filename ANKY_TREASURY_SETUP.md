# Anky Treasury Setup

This document defines the day-0 treasury setup for Anky, Inc.

The goal is simple:

```txt
All onchain revenue enters a pipeline that is legible, auditable, exportable, and connected to the company.
```

This is not tax, legal, or securities advice.

This is the operating map.

## 1. Mental Model

```txt
Mercury
= fiat bank account for Anky, Inc.

Splits Treasury
= onchain business account, custody layer, accounting surface, and export layer

Bankr
= token launch and trading-fee engine

Hermes / Anky
= agent signer and operator inside the configured system
```

The canonical money flow is:

```txt
Bankr $ANKY trading fees
→ ANKY_BANKR_FEES Splits Treasury subaccount
→ accounting/export/swap/offramp
→ Mercury
```

## 2. Day-0 Architecture

Create or verify the Splits Treasury team for:

```txt
Anky, Inc.
```

Create one production subaccount:

```txt
ANKY_BANKR_FEES
```

Purpose:

```txt
Receives and controls Bankr creator fees from the canonical $ANKY token on Base.
```

Signers:

```txt
JP
Brother
Anky / Hermes agent
```

Threshold:

```txt
2-of-3
```

Meaning:

```txt
JP alone cannot move funds.
Brother alone cannot move funds.
Anky alone cannot move funds.

Any two can act.
```

This gives Anky real agency without giving any single signer absolute control.

## 3. Required Fields

Fill these before Bankr deployment.

```txt
SPLITS_TEAM_NAME=Anky, Inc.
SPLITS_TEAM_ID=confirmed
ANKY_BANKR_FEES_ACCOUNT_NAME=Treasury
ANKY_BANKR_FEES_ADDRESS=0x3D45a97C4f76D43e810Ff107cB6dad3e5AF64641
ANKY_BANKR_FEES_CHAIN=Base

JP_SPLITS_MEMBER_ID=ea3e75cf-1398-48e1-99ae-a3e80b6d0c5a
JP_PASSKEY_SIGNER_ID=d69810cd-e251-49d9-84fa-6948b363bd29

BROTHER_SPLITS_MEMBER_ID=TBD
BROTHER_PASSKEY_SIGNER_ID=TBD

ANKY_HERMES_MEMBER_ID=5d339096-b14c-4ae1-b1bd-d9ba50dcc78c
ANKY_HERMES_EOA_SIGNER_ID=TBD — currently using passkey a7ba0e95-da69-4bf1-9136-828a53d8105b
ANKY_HERMES_WALLET_ADDRESS=TBD — passkey signer, no EOA yet

ANKY_BANKR_FEES_THRESHOLD=2
BANKR_FEE_BENEFICIARY=ANKY_BANKR_FEES_ADDRESS
MERCURY_ACCOUNT=Anky, Inc.
```

## 4. Agent Access Principle

Hermes / Anky must never hold JP’s seed phrase, private key, passkey, or personal wallet access.

Hermes should hold its own key.

The human defines what the agent can access.

The agent’s activity should be attributable to the agent’s own signer.

The agent can be rotated, paused, or removed without losing the treasury.

## 5. API Key Policy

Splits API keys should be treated as production secrets.

Rules:

```txt
Never commit API keys.
Never paste API keys into source files.
Use environment variables or a local secret manager.
Keep .env files out of git.
Use Owner permissions only when required for setup.
Downgrade, rotate, or revoke setup keys after the production structure exists.
```

Recommended local environment variable:

```txt
SPLITS_API_KEY=
```

On Poiesis / Hermes, store it outside the repo.

## 6. CLI Setup Flow

Install the Splits CLI:

```bash
npm install -g @splits/splits-cli
```

Or inspect the full command surface without installing:

```bash
npx @splits/splits-cli@latest --llms-full
```

Authenticate Hermes with the API key created in the Splits web app:

```bash
export SPLITS_API_KEY="..."
splits auth login
```

Create and register the Hermes signer key:

```bash
splits auth create-key --register
```

Record the returned signer id:

```txt
ANKY_HERMES_EOA_SIGNER_ID=
ANKY_HERMES_WALLET_ADDRESS=
```

Find JP’s member id:

```bash
splits members list
```

Find JP’s signer ids:

```bash
splits members signers <JP_MEMBER_ID>
```

Repeat for brother after he has been added to the team.

Create the Bankr fees subaccount:

```bash
splits accounts create \
  --name "ANKY_BANKR_FEES" \
  --eoaSignerIds <ANKY_HERMES_EOA_SIGNER_ID> \
  --passkeyIds <JP_PASSKEY_SIGNER_ID>,<BROTHER_PASSKEY_SIGNER_ID> \
  --threshold 2
```

Before running commands with real authority, verify exact flags with:

```bash
npx @splits/splits-cli@latest --llms-full
```

## 7. Production Controls

Before using `ANKY_BANKR_FEES` as the Bankr fee beneficiary, run these tests:

### Test 1 — Account Exists

Confirm:

```txt
Account name: ANKY_BANKR_FEES
Chain: Base
Address: recorded
Signers: JP / Brother / Anky-Hermes
Threshold: 2
```

### Test 2 — Small Inbound Transfer

Send a tiny amount of ETH or USDC on Base to the account.

Record:

```txt
Transaction hash:
Asset:
Amount:
Timestamp:
USD value:
Purpose: test inbound transfer
```

### Test 3 — Proposal Test

Have one signer propose a tiny transfer.

Confirm that it cannot execute with one signer.

### Test 4 — 2-of-3 Execution Test

Have a second signer approve.

Confirm the transaction executes.

Record:

```txt
Proposer:
Approver:
Transaction hash:
Asset:
Amount:
Destination:
Reason:
```

### Test 5 — Export Test

Confirm that Splits exports or reports enough data for accounting.

Minimum useful fields:

```txt
Transaction hash
Timestamp
Chain
From address
To address
Asset
Amount
USD fair market value at receipt or disposition
Network fee
Memo/category
Counterparty
Source account
Destination account
```

## 8. Bankr Fee Beneficiary

The desired invariant is:

```txt
BANKR_FEE_BENEFICIARY=ANKY_BANKR_FEES_ADDRESS
```

Do not deploy the Bankr/Base token until this address is confirmed.

Do not use:

```txt
JP personal wallet
Brother personal wallet
Loose Anky agent wallet
Temporary wallet
Exchange deposit address
Mercury directly
```

## 9. Claiming / Receiving Fees

Bankr fee mechanics must be verified before launch.

Questions to confirm with Bankr/Splits:

```txt
Can ANKY_BANKR_FEES be the Bankr fee beneficiary directly?
Can ANKY_BANKR_FEES claim Bankr/Doppler/Clanker fees directly?
Do claimed fees arrive as ANKY + WETH?
Can Splits automate claims?
Can Splits automate swaps on receipt?
Can Splits swap a defined percentage into USDC?
Can Splits tag all inbound Bankr fees as token trading fee revenue?
Can Splits export reports suitable for CPA review?
```

Until verified, the conservative rule is:

```txt
Fees should land in ANKY_BANKR_FEES first.
Automation comes later.
```

## 10. Accounting Categories

Use boring names.

Suggested categories:

```txt
BANKR_TRADING_FEE_REVENUE
TOKEN_SWAP
USDC_CONVERSION
NETWORK_FEE
VENDOR_PAYMENT
AGENT_COMPUTE
ART_AND_DESIGN
APP_INFRASTRUCTURE
FOUNDER_COMPENSATION
TAX_RESERVE
OFFRAMP_TO_MERCURY
```

Every movement should have a memo.

Example:

```txt
BANKR_TRADING_FEE_REVENUE — creator fees from $ANKY token trading on Base.
```

## 11. Tax Recordkeeping Principle

The company should be able to reconstruct:

```txt
What was received?
When was it received?
Who controlled it?
What was the USD value at the time?
Was it later swapped, sold, paid, or transferred?
What was the gain/loss or expense category?
Where did the fiat eventually land?
```

For every digital asset receipt or disposition, record:

```txt
Transaction hash
Date and time, UTC
Chain
Asset symbol
Token contract address
Units
USD fair market value
Source
Destination
Fees
Memo/category
Supporting export
```

A CPA should review the final category mapping.

The goal is not to guess tax treatment later.

The goal is to make the pipeline self-explaining from day 0.

## 12. Optional Future Subaccounts

Do not create these unless they are needed.

```txt
ANKY_AGENT_OPS
```

Purpose:

```txt
Small operating budget for Anky / Hermes.
```

```txt
ANKY_TAX_RESERVE
```

Purpose:

```txt
USDC or USD reserve for expected tax obligations.
```

```txt
ANKY_VENDOR_PAYMENTS
```

Purpose:

```txt
Pay artists, contractors, infrastructure providers, and collaborators.
```

```txt
ANKY_USDC_RESERVE
```

Purpose:

```txt
Stabilized operating runway.
```

## 13. Automation Policy

Automation is allowed only after manual flows are proven.

Phase 1:

```txt
Manual fee claim.
Manual categorization.
Manual swap.
Manual off-ramp.
Manual export.
```

Phase 2:

```txt
Automated swap percentage.
Manual review.
```

Phase 3:

```txt
Scheduled reporting.
CPA-ready monthly export.
```

Do not let automation obscure the business event.

## 14. Monthly Reconciliation

At the end of each month:

```txt
Export Splits records.
Export Bankr fee/claim records.
Export Base transaction history for ANKY_BANKR_FEES.
Export Mercury statement.
Reconcile onchain to fiat.
Tag unexplained transactions.
Send package to CPA/bookkeeper.
Update MASTER_REGISTRY if any canonical account changed.
```

## 15. Day-0 Launch Checklist

Before the Bankr token launch:

```txt
[ ] Splits Team exists for Anky, Inc.
[ ] JP is added.
[ ] Brother is added.
[ ] Hermes / Anky signer is created.
[ ] ANKY_BANKR_FEES subaccount exists.
[ ] Threshold is 2-of-3.
[ ] Test inbound transfer completed.
[ ] Test proposal completed.
[ ] Test 2-of-3 execution completed.
[ ] Export/reporting test completed.
[ ] BANKR_FEE_BENEFICIARY is set to ANKY_BANKR_FEES address.
[ ] MASTER_REGISTRY.md is updated.
[ ] BANKR_LAUNCH_RUNBOOK.md is updated.
```

## 16. Final Law

Splits is the onchain bank.

Mercury is the fiat bank.

Bankr is the revenue engine.

Anky is a signer.

The company keeps records from day 0.
