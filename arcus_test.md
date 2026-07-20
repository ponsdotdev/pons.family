# Arcus ($ARCUS)
### The first arch of pons.family

> *"Every bridge stands because of its arch."*

**Contract Address (CA):** `0x6e4db65db8758d943f61d2f9abcb26449b93082d`

> ⚠️ **Arcus is a protocol test token. It has no holder utility.**

---

# 1. What Is Arcus?

**Arcus** is the canonical reference test token of **pons.family**.

Its name comes from the Latin word **_arcus_**, meaning **arch**—the structural element that allows a bridge to exist by distributing its load into stable foundations.

Long before a bridge becomes a path, it is simply an arch proving that the structure can support itself.

That is exactly what **$ARCUS** represents.

It was the very first TEST token deployed through the `PonsLaunchFactory`, created exclusively to validate the complete lifecycle of the protocol before any production launch.

Every rule, every restriction, every liquidity operation, and every graduation check was intentionally exercised using a single deterministic deployment.

Arcus is not the destination.

It is the proof that the bridge can stand.

---

# 2. The Origin

Every protocol begins with uncertainty.

Before pons.family could launch real assets, it first needed to answer one fundamental question:

> **Can every component of the protocol work together exactly as intended?**

The answer became **Arcus**.

No announcement.

No marketing.

No speculation.

Only a single controlled execution of `launchToken()` inside the protocol environment.

That deployment became the reference execution against which every future version of pons.family can be compared.

From the creation of the ERC-20 contract to liquidity initialization, anti-snipe enforcement, deterministic deployment, graduation tracking, and permanent launch records, every subsystem was verified through the lifecycle of a single token.

Arcus was never intended to create value.

Its purpose was to create confidence.

---

# 3. Why "Arcus"

The Latin word **_arcus_** describes the architectural arch—the defining element that allows a bridge to transfer force into stability.

Without an arch, a bridge collapses under its own weight.

Without a canonical reference deployment, a launch protocol cannot confidently evolve.

Arcus plays that role inside pons.family.

It carries no economic significance.

Its importance is structural.

Every future launcher, contract upgrade, and protocol iteration can be measured against the behavior originally established by Arcus.

---

# 4. Protected Launch Lifecycle

Arcus was intentionally launched under the protocol's strictest protection rules.

For the first ten blocks:

- wallets could not accumulate more than **2%** of supply;
- transactions were capped at **2.2%** of supply;
- launch-block sniping was prevented except for the designated initial liquidity recipient.

These protections were never manually disabled.

They expired automatically because the protocol completed the lifecycle it was programmed to execute.

The launch itself became proof that restriction logic, state transitions, and automated protection windows behaved deterministically.

---

# 5. Canonical Fixture Specification

Arcus is intentionally reproducible.

Every parameter below exists to provide a stable reference across future protocol versions.

## Token Identity

| Field | Value | Purpose |
|---|---|---|
| `name` | Arcus | Canonical protocol reference token |
| `symbol` | ARCUS | Latin for "arch" |
| `logo` | `ipfs://arcus-logo` | Stable placeholder |
| `description` | *Canonical launch fixture for the pons.family protocol* | Reference deployment |
| `feeWallet` | unset | Default protocol behavior |

Social metadata (`telegram`, `discord`, `farcaster`) intentionally remains empty to demonstrate that external metadata is optional and never affects protocol behavior.

---

# 6. Launch Configuration

| Parameter | Value | Purpose |
|---|---|---|
| `initialTick` | `-60000` | Deterministic pool initialization |
| `tickSpacing` | `60` | Standard V3 spacing |
| `poolFee` | `3000` | Standard fee tier |
| `maxWalletBps` | `200` | Wallet protection |
| `maxTxBps` | `220` | Transaction protection |
| `restrictionBlocks` | `10` | Anti-snipe lifecycle |
| `supply` | `1,000,000` | Basis-point validation |
| `graduationThreshold` | `10 ether` | Graduation testing |

---

# 7. Reference Validation Variants

Each variant changes a single parameter while preserving every other launch condition.

| Variant | Modification | Expected Result |
|---|---|---|
| Invalid BPS | `maxTxBps → 221` | Configuration rejected |
| Zero Supply | `supply → 0` | Launch rejected |
| Missing Pair Token | zero address | Launch rejected |
| Disabled Configuration | `enabled → false` | Deployment blocked |
| Graduation Disabled | threshold = `0` | Token never graduates |
| Legacy Router | alternate router | Router compatibility verification |

Together, these fixtures define the protocol's expected failure conditions.

---

# 8. Contract Architecture

Arcus exists to validate the interaction between the protocol's two primary contracts.

---

## 8.1 PonsLaunchFactory

The orchestration layer responsible for the entire deployment lifecycle.

| Function | Responsibility |
|---|---|
| `launchToken()` | Complete launch execution |
| `predictTokenAddress()` | Deterministic deployment |
| `graduationStatus()` | Graduation verification |
| `getLaunchedToken()` | Permanent launch registry |
| `addDexConfig()` | Infrastructure registration |
| `addLaunchConfig()` | Launch configuration |
| `setLaunchEnabled()` | Launch permissions |
| `setWhitelistedLauncher()` | Authorized launchers |

---

## 8.2 PonsLauncherToken

The token implementation responsible for launch-time protections.

| Function | Responsibility |
|---|---|
| `constructor()` | Supply creation & metadata |
| `_update()` | Restriction enforcement |
| `liquidityPool()` | Canonical pool discovery |
| `maxWalletLimit()` | Wallet restriction |
| `maxTxLimit()` | Transaction restriction |
| `setInitialBuyRecipient()` | Seed buyer authorization |
| `socials()` | Frontend metadata |
| `_isPairPool()` | Pool validation |

---

# 9. What Arcus Proves

Arcus serves as the protocol's permanent reference deployment.

It demonstrates that:

- deterministic deployments remain reproducible;
- liquidity initialization behaves consistently;
- launch protections execute exactly once;
- graduation is derived from real on-chain liquidity;
- launch records remain permanently verifiable;
- future protocol versions preserve behavioral compatibility.

Every new version of pons.family can recreate Arcus and compare its execution against the original reference.

If Arcus behaves identically, the protocol's guarantees remain intact.

---

# 10. The Role of Arcus

Arcus is not a community token.

It is not a governance asset.

It is not an investment.

Its purpose is infrastructure.

As pons.family evolves, Arcus becomes the canonical benchmark used to validate new launch configurations, factory upgrades, liquidity systems, lockers, and deployment logic.

Just as engineers test new bridge designs against proven structural principles, every future iteration of pons.family can be measured against the first arch that proved the system could stand.

---

> *An arch is rarely the part people remember.*
>
> *Yet without it, nothing crosses the river.*

**Arcus ($ARCUS)**  
*The first arch of pons.family.*  
*Protocol reference deployment. Test token. No holder utility.*
