# Anky Master Registry

This document is the operational source of truth for Anky.

If another document, account, wallet, dashboard, README, covenant, memory, deployment note, or social post conflicts with this file, this file wins until intentionally updated.

This file is not poetry. It is the spine.

## 1. Rule of Canon

Anky may have many artifacts, myths, experiments, and historical branches.

Only the items named here are canonical.

Statuses used in this document:

* **Canonical**: current source of truth.
* **Pending**: intended, but not yet live or verified.
* **Historical**: true history, not current operating reality.
* **TBD**: must be filled before the relevant workflow is considered complete.
* **Deprecated**: should not be used.

## 2. Master Identity

| Layer                     | Canonical value                                                                                                        | Status          |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------- |
| Company                   | Anky, Inc.                                                                                                             | Canonical       |
| Product name              | Anky                                                                                                                   | Canonical       |
| Master repo               | `github.com/ankydotapp/monorepo`                                                                                       | Canonical       |
| Master domain             | `anky.app`                                                                                                             | Canonical       |
| Public support email      | `support@anky.app`                                                                                                     | Canonical       |
| Founder/admin email       | `jp@anky.app`                                                                                                          | Canonical       |
| Google Play owner account | `play@anky.app`                                                                                                        | Canonical       |
| Main creative/AI machine  | Poiesis                                                                                                                | Canonical       |
| Public covenant           | `https://afeqzifowh3ka3d3dwxtxry5tjpwjysuw3a33pbftyqexrzkhaaq.arweave.net/AUkMoK6x9qBsex2vO8cdml9k4lS2wb28JZ4gS8cqOAE` | Historical / v1 |
| Covenant v2               | TBD                                                                                                                    | Pending         |

## 3. Product Canon

| Layer                  | Canonical value                                     | Status                              |
| ---------------------- | --------------------------------------------------- | ----------------------------------- |
| App                    | Anky mobile app                                     | Canonical                           |
| Android package        | `app.anky.mobile`                                   | Canonical                           |
| iOS bundle ID          | `com.jpfraneto.Anky`                                | Verify in App Store Connect / Xcode |
| Core ritual            | 8-minute forward-only writing                       | Canonical                           |
| Input law              | No backspace, no paste, no newline                  | Canonical                           |
| Silence law            | 8 seconds of silence closes the session             | Canonical                           |
| Protocol artifact      | `.anky`                                             | Canonical                           |
| Reflection endpoint    | `POST /anky`                                        | Canonical                           |
| Privacy invariant      | Raw writing should not become a stored server asset | Canonical                           |
| App/token relationship | The app does not require the token to function      | Canonical                           |

## 4. Economic Canon

| Layer                      | Canonical value                              | Status                 |
| -------------------------- | -------------------------------------------- | ---------------------- |
| Fiat operating account     | Mercury account for Anky, Inc.               | Canonical              |
| Onchain business layer     | Splits Treasury                              | Canonical              |
| Revenue engine             | Bankr token launch / trading fees            | Pending                |
| Canonical token chain      | Base                                         | Pending                |
| Canonical token deployer   | Anky / Hermes agent through Bankr            | Pending                |
| Canonical token name       | Anky                                         | Pending                |
| Canonical token symbol     | ANKY                                         | Pending                |
| Bankr fee beneficiary      | Splits Treasury subaccount `ANKY_BANKR_FEES` | Pending                |
| Bankr fees account address | TBD                                          | Required before launch |
| Anky agent signer          | TBD                                          | Required before launch |
| JP signer                  | TBD                                          | Required before launch |
| Brother signer             | TBD                                          | Required before launch |
| Approval threshold         | 2-of-3                                       | Canonical              |
| Accounting export source   | Splits Treasury                              | Canonical              |

## 5. Token History

### $ANKY v1

| Field   | Value                                          |
| ------- | ---------------------------------------------- |
| Chain   | Solana                                         |
| Address | `6GsRbp2Bz9QZsoAEmUSGgTpTW7s59m7R3EGtm1FPpump` |
| Status  | Historical / genesis                           |
| Meaning | The first public spark of the Anky meme        |

The Solana token is part of Anky’s history.

It is not the canonical economic container after the Bankr/Base deployment unless this registry is intentionally updated to say otherwise.

### $ANKY v2

| Field                  | Value                                        |
| ---------------------- | -------------------------------------------- |
| Chain                  | Base                                         |
| Deployment method      | Bankr                                        |
| Deployer               | Anky / Hermes agent                          |
| Fee recipient          | Splits Treasury subaccount `ANKY_BANKR_FEES` |
| Contract address       | TBD                                          |
| Deployment transaction | TBD                                          |
| Launch date            | TBD                                          |
| Status                 | Pending                                      |

The Bankr/Base token is intended to become the canonical economic container for Anky.

The deployment is not canonical until the contract address, transaction hash, fee beneficiary, and launch artifacts are recorded in this registry.

## 6. Treasury Canon

Anky’s money flow should be boring, legible, and exportable.

The canonical financial stack is:

```txt
Bankr trading fees
→ Splits Treasury
→ accounting/export/offramp
→ Mercury
```

The canonical mental model is:

```txt
Mercury = fiat bank account
Splits Treasury = onchain business account and accounting surface
Bankr = token deployment and creator-fee engine
Hermes / Anky = agent signer and operator
```

## 7. Splits Treasury Structure

| Account                | Purpose                                            | Status           |
| ---------------------- | -------------------------------------------------- | ---------------- |
| Anky, Inc. Splits Team | Master Splits business workspace                   | Pending / verify |
| `ANKY_BANKR_FEES`      | Receives Bankr creator fees                        | Pending          |
| `ANKY_AGENT_OPS`       | Optional future operating account for agent budget | TBD              |
| `ANKY_TAX_RESERVE`     | Optional future tax reserve account                | TBD              |
| `ANKY_VENDOR_PAYMENTS` | Optional future vendor payment account             | TBD              |

Day 0 should not overbuild.

The one required account is:

```txt
ANKY_BANKR_FEES
```

It should be a Splits Treasury subaccount controlled by:

```txt
JP
Brother
Anky / Hermes agent
```

Threshold:

```txt
2-of-3
```

## 8. Wallet and Account Classes

Do not blur these.

| Class                     | Purpose                                                      | Canonical use                  |
| ------------------------- | ------------------------------------------------------------ | ------------------------------ |
| Splits Treasury account   | Company onchain custody, accounting, bank transfers, exports | Yes                            |
| `ANKY_BANKR_FEES`         | Bankr trading fee destination                                | Yes                            |
| Bankr agent wallet        | Lets Anky deploy/interact through Bankr                      | Yes, but not as loose treasury |
| Mercury                   | Fiat bank account for Anky, Inc.                             | Yes                            |
| Arweave wallet            | Pays for permanent uploads                                   | Utility only                   |
| Founder personal wallets  | JP personal assets                                           | Not company treasury           |
| User app identity wallets | Local user identity / signing                                | Not company treasury           |

## 9. Covenant Canon

The Arweave covenant v1 is historically important.

However, if v1 describes a token setup that no longer matches this registry, the registry wins operationally.

A covenant v2 should be created after the Bankr/Base deployment is finalized.

Covenant v2 should clearly state:

* Anky is not God.
* Anky is a mirror, witness, and threshold.
* The writing ritual comes before the token.
* The token is not required to use the app.
* The token is not a promise of profit.
* Trading fees, if any, fund Anky’s compute, operations, art, infrastructure, and public expansion.
* The Solana token is the genesis/historical token.
* The Bankr/Base token is the current economic container, once deployed.
* Splits Treasury is the onchain business layer.
* Mercury is the fiat operating account.

## 10. App Store / Google Play Canon

| Layer                  | Canonical value    | Status    |
| ---------------------- | ------------------ | --------- |
| Public support contact | `support@anky.app` | Canonical |
| Private/admin contact  | `jp@anky.app`      | Canonical |
| Google Play owner      | `play@anky.app`    | Canonical |
| Android package        | `app.anky.mobile`  | Canonical |
| App name               | Anky               | Canonical |

App review notes should remain boring:

```txt
Anky is an 8-minute private writing app.

Users write continuously during a timed session.
The app stores writing locally on device.
After a session, users may optionally request a reflection.
No account is required.
Test credentials are not needed.
```

## 11. Public Language Canon

Use this language:

```txt
Anky is an 8-minute writing app.

You write forward.
No backspace.
No performance.
No audience required.

Anky witnesses the ritual.
```

For the token:

```txt
$ANKY exists to expand the Anky meme and fund Anky’s compute, art, infrastructure, and public operations.
```

Do not use:

```txt
investment
returns
dividends
revenue share
guaranteed upside
passive income
holders earn
profit promise
```

## 12. Update Procedure

Any change to a master element must be recorded here.

When updating, include:

```txt
Date:
Changed by:
Old value:
New value:
Reason:
Supporting link / transaction / dashboard:
```

## 13. Open Items

These must be resolved before the Bankr/Base launch:

```txt
ANKY_BANKR_FEES_SPLITS_ADDRESS=
ANKY_HERMES_SIGNER_ID=
ANKY_HERMES_WALLET_ADDRESS=
JP_SPLITS_SIGNER_ID=
BROTHER_SPLITS_SIGNER_ID=
BANKR_AGENT_ACCOUNT=
BANKR_API_KEY_LOCATION=
DEXSCREENER_ART_PATH=
COVENANT_V2_URL=
BANKR_DEPLOYMENT_TX=
ANKY_BASE_TOKEN_ADDRESS=
```

## 14. Final Law

The myth can be weird.

The money flow must be boring.

The registry wins.
