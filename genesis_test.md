# Pons Genesis ($GENESIS)
### Canonical protocol test token

> *"Every protocol needs a genesis before production begins."*

**Contract Address (CA):** `0xebe68bdf4dd9af35d3816b2bdb7b9ab96c073356`

> ⚠️ **This is a protocol test token. It has no holder utility and is not intended for trading.**

---

# 1. What It Is

**Pons Genesis** is the canonical test token of **pons.family**, created by the `PonsLaunchFactory` to validate the protocol's complete launch lifecycle.

It was never designed for trading.

Instead, `$GENESIS` exists as a deterministic reference asset for development, testing, and protocol verification.

Every parameter of its launch—including graduation threshold, anti-snipe protection, wallet limits, liquidity behavior, and deployment flow—was intentionally selected to exercise the protocol under controlled conditions and verify that every component behaves exactly as designed.

The name **Genesis** reflects its purpose within the development process.

Not because it was the first token ever launched on pons.family, but because it represents the canonical starting point whenever the launch system must be validated from a clean state.

Every future version of the protocol can recreate `$GENESIS` and compare its behavior against this reference configuration, ensuring deterministic and reproducible launches across upgrades.

---

# 2. The Story

Every launchpad needs a reliable way to verify that its infrastructure behaves correctly before real projects depend on it.

That role belongs to **Pons Genesis**.

No announcement.

No public launch.

No speculation.

Only a controlled `launchToken()` execution performed inside the protocol environment, creating a reusable reference asset for testing every critical mechanism behind the platform.

`$GENESIS` validates the complete launch lifecycle—from deployment and liquidity creation to launch restrictions, anti-snipe protection, and graduation logic—using exactly the same execution path as a production launch.

For ten blocks, `$GENESIS` operates under the protocol's launch protections:

- wallets cannot accumulate more than 2% of supply from the pool;
- individual transactions are limited to 2.2% of supply;
- launch-block sniping is prevented unless executed through the designated seed-buy flow.

When the restriction period expires, every safeguard is removed automatically.

No administrator intervenes.

No manual action is required.

The protocol simply completes the lifecycle it was designed to execute.

Because the configuration is deterministic, `$GENESIS` can be recreated whenever the protocol evolves, providing a stable benchmark for future versions of the launchpad.

---

# 3. Fixture Specification

Every parameter below exists for a technical reason.

This configuration is the canonical blueprint used to reproduce `$GENESIS` across test environments, protocol versions, and future factory iterations.

## Token Identity

| Field | Value | Notes |
|---|---|---|
| `name` | Pons Genesis | Canonical protocol test token |
| `symbol` | GENESIS | Reference launch fixture |
| `logo` | `ipfs://pons-genesis-logo` | Stable placeholder |
| `description` | *Canonical genesis fixture for the pons.family test suite* | Protocol reference asset |
| `feeWallet` | unset by default | Default fee collection behavior |

Social fields remain intentionally blank, proving the protocol does not require external metadata.

---

# 4. Launch Parameters

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

# 5. Derived Negative-Path Variants

Each variant changes exactly one parameter from the `$GENESIS` reference configuration.

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

`$GENESIS` is created and controlled by two main contracts.

## 6.1 `PonsLaunchFactory` — The Launch Engine

| Function | Role for $GENESIS |
|---|---|
| `launchToken(TokenParams, launchConfigId, dexId, salt)` | Deploys `$GENESIS`, creates the token, initializes liquidity, creates the V3 position, assigns the locker, and executes the launch flow atomically |
| `predictTokenAddress(...)` | Calculates deterministic deployment addresses before launch |
| `graduationStatus(token)` | Verifies graduation using locked liquidity position data |
| `getLaunchedToken(token)` | Returns the permanent on-chain record of `$GENESIS` |
| `addDexConfig` / `addLaunchConfig` | Registers required launch infrastructure |
| `setLaunchEnabled` / `setWhitelistedLauncher` | Controls launch permissions |

## 6.2 `PonsLauncherToken` — The Reference Asset

| Function | Role for $GENESIS |
|---|---|
| `constructor(...)` | Creates the fixed supply, records launch state, and stores metadata |
| `_update(from, to, value)` | Executes anti-snipe and restriction logic |
| `liquidityPool()` | Resolves the canonical liquidity pool |
| `maxWalletLimit()` / `maxTxLimit()` | Calculates active restrictions |
| `setInitialBuyRecipient(address)` | Temporarily allows the initial seed buyer |
| `socials()` / `getTokenInfo()` | Provides frontend-readable metadata |
| `_isPairPool(candidate)` | Detects valid protocol pools |

---

# 7. What $GENESIS Actually Proves

- Canonical reference configuration for launch testing.
- Graduation validation using real locked liquidity.
- Complete anti-snipe lifecycle verification.
- Deterministic protocol behavior across upgrades.
- Infrastructure compatibility for future launchpad versions.

---

# 8. The Future of $GENESIS

**To be completely clear: `$GENESIS` is a protocol test token with no holder utility today.**

It is not marketed, not designed for speculation, and not intended as an investment asset.

Its purpose is entirely protocol-focused:

- Launchpad evolution through reproducible testing.
- Living documentation of the complete launch flow.
- Infrastructure certification for future protocol components.
- Canonical reference implementation for developers and auditors.

Every protocol needs a reproducible beginning.

For pons.family, that beginning is **Genesis**.

---

*Pons Genesis ($GENESIS) — canonical protocol test token. No holder utility today. Permanent reference implementation for the pons.family launchpad.*
