# Pons Arch ($ARCH) Test Token
### The first arch of pons.family

> *"Every bridge needs an arch to carry its weight."*

**Contract Address (CA):** `0x8620aadd8b94d15aafd57de4c619686fef9e6575`

> ⚠️ **This is a test token.**

---

## 1. What It Is

**Pons Arch** is the canonical test token of [pons.family](https://pons.family) — the first `$ARCH` ever created by the `PonsLaunchFactory`.

It was never designed for trading. It was designed to **validate the foundations** of the protocol.

Every parameter of its launch — graduation threshold, anti-snipe protection, wallet limits, liquidity behavior, and deployment flow — was intentionally chosen to push the system against its own boundaries and verify that every component behaves exactly as designed.

The name comes from architecture: an **arch** is a structure that distributes pressure across its supports, allowing a bridge to stand without collapsing under its own load.

That is the role of `$ARCH` inside pons.family: not a destination, but the structural element that proves the bridge can hold.

---

## 2. The Story

Before pons.family had users, launches, or production deployments, it had a single question:

*"Can the protocol launch itself correctly?"*

The answer became **Pons Arch**.

No public announcement. No market launch. No speculation.

Just a controlled `launchToken()` execution from the protocol environment, creating the first reference asset used to test every critical mechanism behind the platform.

`$ARCH` became the first structural checkpoint of the system — the token used to verify that deployments, liquidity creation, restrictions, and graduation logic all worked together as intended.

For ten blocks, `$ARCH` operated under the strictest rules enforced by the protocol:

- wallets could not accumulate more than 2% of supply from the pool;
- single transactions were limited to 2.2% of supply;
- launch-block sniping was blocked unless coming from the designated seed-buy flow.

After the restriction period expired, the controls disappeared automatically — not because an administrator disabled them, but because the protocol completed the lifecycle it was designed to execute.

From that moment, `$ARCH` became what every future pons.family launch would inherit: a proven foundation.

---

## 3. Fixture Specification

Every parameter below exists for a technical reason.

This configuration is the reference blueprint used to reproduce `$ARCH` across test environments, protocol versions, and future factory iterations.

### Token identity

| Field | Value | Notes |
|---|---|---|
| `name` | Pons Arch | First structural reference token of pons.family |
| `symbol` | ARCH | Represents the architectural foundation of the protocol |
| `logo` | `ipfs://pons-arch-logo` | Stable placeholder |
| `description` | *"Canonical genesis fixture for the pons.family test suite"* | Explicitly a protocol test asset |
| `feeWallet` | unset by default | Default fee collection behavior |

Social fields (`telegram`, `discord`, `farcaster`) remain intentionally blank, proving that the protocol does not require external social metadata.

---

## 4. Launch Parameters

| Parameter | Value | What it tests |
|---|---|---|
| `initialTick` | `-60000` | Negative tick boundary and deterministic range calculations |
| `tickSpacing` | `60` | Consistency with V3 pool configuration |
| `poolFee` | `3000` | Standard Uniswap V3 fee tier |
| `maxWalletBps` | `200` (2%) | Wallet restriction logic |
| `maxTxBps` | `220` | Transaction limit validation |
| `restrictionBlocks` | `10` | Full anti-snipe lifecycle testing |
| `supply` | `1,000,000` | Safe supply floor for basis-point calculations |
| `graduationThreshold` | `10 ether` | Controlled graduation testing |

---

## 5. Derived Negative-Path Variants

Each variant changes exactly one parameter from the `$ARCH` reference configuration.

| Variant | Change | Expected result |
|---|---|---|
| Invalid bps | `maxTxBps` → 221 | Configuration rejected |
| Zero supply | `supply` → 0 | Launch rejected |
| Missing pair token | `pairToken` → zero address | Launch rejected |
| Disabled config | `enabled` → false | Launch blocked |
| No graduation | `graduationThreshold` → 0 | Never considered graduated |
| Deadline router | DEX-side variant | Tests classic V3 router handling |

---

# 6. Contract Technical Reference

$ARCH is created and controlled by two main contracts.

This section documents the components responsible for its lifecycle.

---

## 6.1 `PonsLaunchFactory` — The Foundation Layer

| Function | Role for $ARCH |
|---|---|
| `launchToken(TokenParams, launchConfigId, dexId, salt)` | Deploys `$ARCH`, creates the token, initializes liquidity, creates the V3 position, assigns the locker, and executes the launch flow atomically |
| `predictTokenAddress(...)` | Calculates deterministic deployment addresses before launch |
| `graduationStatus(token)` | Verifies graduation using locked liquidity position data |
| `getLaunchedToken(token)` | Returns the permanent on-chain record of `$ARCH` |
| `addDexConfig` / `addLaunchConfig` | Registers the required launch infrastructure |
| `setLaunchEnabled` / `setWhitelistedLauncher` | Controls launch permissions |

---

## 6.2 `PonsLauncherToken` — The Structural Element

| Function | Role for $ARCH |
|---|---|
| `constructor(...)` | Creates the fixed supply, records launch state, and stores metadata |
| `_update(from, to, value)` | Executes the anti-snipe and restriction logic during the protected window |
| `liquidityPool()` | Resolves the canonical liquidity pool |
| `maxWalletLimit()` / `maxTxLimit()` | Calculates active restrictions |
| `setInitialBuyRecipient(address)` | Temporarily allows the initial seed buyer |
| `socials()` / `getTokenInfo()` | Provides frontend-readable metadata |
| `_isPairPool(candidate)` | Detects valid protocol pools |

---

# 7. What $ARCH Actually Proves

- **Reference foundation** — every future launch configuration can be compared against `$ARCH`.
- **Graduation validation** — proves that graduation reads real locked liquidity.
- **Anti-snipe verification** — the first complete lifecycle test of launch restrictions.
- **Protocol continuity check** — future factory versions can reproduce `$ARCH` to verify compatibility.

---

# 8. The Future of $ARCH

**To be completely clear: `$ARCH` is a test token today, with no holder utility.**

It is not marketed, not designed for speculation, and not intended as an investment asset.

Its purpose is entirely protocol-focused:

- **Launchpad evolution** — every new `PonsLaunchFactory` version can recreate `$ARCH` to verify behavioral consistency.
- **Living documentation** — `$ARCH` becomes the canonical example of how pons.family launches work.
- **Infrastructure certification** — new locker and launch components must prove compatibility against `$ARCH`.

An arch does not exist to be admired.

It exists to support everything built on top of it.

---

*Pons Arch ($ARCH) — the first arch supports the bridge. Test token. No holder utility today. Protocol reference standard, permanently.*