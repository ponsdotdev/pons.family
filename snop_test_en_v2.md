# Snop ($SNOP)
### The mirror image of ponsfamily.com

> *"Every bridge has a reflection, even before it has a shape."*

**Dev Wallet:** `0x698d3e165c1ea84aa23ea02ca8a91f574e4c70eb`

> ⚠️ **Snop is a protocol test token. It has no holder utility.**

**Website:** [ponsfamily.com](https://ponsfamily.com)

---

# 1. What Is Snop?

**Snop** is the quintessential mirror test token of **pons.family**.

Its name is simply **pons** spelled backwards. Where "pons" is the bridge that connects, **snop** is its reflection: the counterpart that lets the same structure be observed from the opposite direction without changing its substance.

A mirror doesn't add anything to the bridge. It just confirms the shape holds, repeated identically no matter which way you look at it.

That's what **$SNOP** represents.

It was the first mirrored TEST token deployed through `PonsLaunchFactory`, created to validate the full lifecycle of the protocol before any production launch. Every rule, restriction, liquidity operation, and graduation check was exercised through a single deterministic deployment.

Snop isn't the destination. It's the reflection proving the bridge holds up, no matter which side you're standing on.

---

# 2. The Origin

Every protocol starts with uncertainty.

Before pons.family could launch real assets, it had to answer one question: does the protocol behave the same way when observed in reverse?

The answer became **Snop**. No announcement, no marketing, no speculation. Just a single controlled execution of `launchToken()` inside the protocol environment.

That deployment became the mirrored reference execution that every future version of pons.family gets compared against. From ERC-20 contract creation to liquidity initialization, anti-snipe enforcement, deterministic deployment, graduation tracking, and permanent launch records, every subsystem was verified through the lifecycle of a single token, read in reverse as well as forward.

Snop was never meant to create value. Its purpose was to create symmetry.

---

# 3. Why "Snop"

**Snop** is **pons**, reversed. Same structure, same logic, opposite direction.

*Pons* is the arch that bears the load and transfers it into stable foundations. *Snop* is the check that confirms the same structure holds when read the other way: from the final result back to the origin.

It carries no economic significance. Its importance is purely structural.

Every future launcher, contract upgrade, and protocol iteration can be measured against the mirrored behavior established by Snop, alongside the direct behavior established by Arcus.

---

# 4. Protected Launch Lifecycle

Snop was launched under the protocol's strictest protection rules.

For the first 10 blocks after deployment:

- **Max wallet:** no address could hold more than 2% of total supply (`maxWalletBps = 200`).
- **Max transaction:** no single transfer could exceed 2.2% of total supply (`maxTxBps = 220`).
- **Anti-snipe:** any buy in the launch block was blocked unless the sender matched the address set via `setInitialBuyRecipient()`.

These restrictions weren't manually lifted. They expired automatically once `restrictionBlocks` elapsed, which is exactly the behavior `_update()` is supposed to enforce. The launch itself is the test case: it proves the restriction logic, the state transitions, and the automatic expiry all execute deterministically, independent of which direction they're inspected from.

---

# 5. Canonical Fixture Specification

Snop is intentionally reproducible. Every parameter below is a stable, mirrored reference point for future protocol versions.

## Token Identity

| Field | Value | Purpose |
|---|---|---|
| `name` | Snop | Mirrored protocol reference token |
| `symbol` | SNOP | "Pons" spelled backwards |
| `logo` | `ipfs://snop-logo` | Stable placeholder URI |
| `description` | *Mirrored launch fixture for the pons.family protocol* | Reference deployment |
| `feeWallet` | `address(0)` (unset) | Default protocol behavior |

Social metadata fields (`telegram`, `discord`, `farcaster`) are left as empty strings intentionally, to confirm that external metadata is optional and never read by the protocol's execution path.

---

# 6. Launch Configuration

| Parameter | Type | Value | Purpose |
|---|---|---|---|
| `initialTick` | `int24` | `-60000` | Deterministic pool initialization price |
| `tickSpacing` | `int24` | `60` | Standard Uniswap V3 spacing |
| `poolFee` | `uint24` | `3000` | 0.3% fee tier |
| `maxWalletBps` | `uint16` | `200` | Wallet cap, basis points (2%) |
| `maxTxBps` | `uint16` | `220` | Transaction cap, basis points (2.2%) |
| `restrictionBlocks` | `uint16` | `10` | Duration of anti-snipe window, in blocks |
| `supply` | `uint256` | `1,000,000 * 10^18` | Total supply, 18 decimals |
| `graduationThreshold` | `uint256` | `10 ether` | Liquidity required to trigger graduation |

---

# 7. Reference Validation Variants

Each variant changes exactly one parameter while holding every other launch condition constant, isolating the failure mode under test.

| Variant | Modification | Expected Result | Reverts With |
|---|---|---|---|
| Invalid BPS | `maxTxBps → 221` | Configuration rejected | `InvalidBps()` |
| Zero Supply | `supply → 0` | Launch rejected | `ZeroSupply()` |
| Missing Pair Token | pair token = `address(0)` | Launch rejected | `InvalidPairToken()` |
| Disabled Configuration | `enabled → false` | Deployment blocked | `LaunchDisabled()` |
| Graduation Disabled | `graduationThreshold → 0` | Token never graduates | *(no revert; graduation check always false)* |
| Legacy Router | alternate router address | Router compatibility verified | *(no revert; behavior comparison only)* |

Together, these fixtures define the protocol's expected failure surface, in its mirrored form. (Revert selector names are illustrative of the pattern the factory enforces; check the deployed ABI for exact identifiers.)

---

# 8. Contract Architecture

Snop validates the interaction between the protocol's two primary contracts, inspected from both directions.

---

## 8.1 PonsLaunchFactory

The orchestration layer responsible for the entire deployment lifecycle.

| Function | Signature | Responsibility |
|---|---|---|
| `launchToken()` | `launchToken(LaunchParams calldata) → address` | Executes a full token launch and returns the deployed address |
| `predictTokenAddress()` | `predictTokenAddress(bytes32 salt, bytes calldata initCode) → address` | Computes the CREATE2 address before deployment |
| `graduationStatus()` | `graduationStatus(address token) → GraduationStatus` | Reads current liquidity vs. `graduationThreshold` |
| `getLaunchedToken()` | `getLaunchedToken(uint256 index) → address` | Reads the permanent on-chain launch registry |
| `addDexConfig()` | `addDexConfig(DexConfig calldata)` | Registers a router/pool factory pair for future launches |
| `addLaunchConfig()` | `addLaunchConfig(LaunchConfig calldata)` | Registers a reusable launch parameter set |
| `setLaunchEnabled()` | `setLaunchEnabled(bool)` | Toggles the global launch permission flag |
| `setWhitelistedLauncher()` | `setWhitelistedLauncher(address, bool)` | Grants or revokes launcher authorization |

---

## 8.2 PonsLauncherToken

The token implementation responsible for launch-time protections.

| Function | Signature | Responsibility |
|---|---|---|
| `constructor()` | `constructor(string name, string symbol, uint256 supply, ...)` | Mints total supply and stores metadata at deploy time |
| `_update()` | `_update(address from, address to, uint256 value) internal override` | Enforces `maxWalletBps` / `maxTxBps` during the restriction window |
| `liquidityPool()` | `liquidityPool() view returns (address)` | Resolves the canonical pool address for this token |
| `maxWalletLimit()` | `maxWalletLimit() view returns (uint256)` | Returns current wallet cap in token units |
| `maxTxLimit()` | `maxTxLimit() view returns (uint256)` | Returns current transaction cap in token units |
| `setInitialBuyRecipient()` | `setInitialBuyRecipient(address)` | Whitelists the address exempt from launch-block anti-snipe |
| `socials()` | `socials() view returns (string, string, string)` | Returns telegram/discord/farcaster metadata for frontends |
| `_isPairPool()` | `_isPairPool(address) internal view returns (bool)` | Validates that a given address is the token's actual liquidity pool, not an arbitrary pair |

---

# 9. What Snop Proves

Snop is the protocol's permanent mirrored reference deployment. It confirms that:

- deterministic deployments stay reproducible whether inspected forward or in reverse;
- liquidity initialization behaves consistently across runs;
- launch protections execute exactly once, for exactly the configured window;
- graduation status is derived strictly from on-chain liquidity, not an external oracle or manual flag;
- launch records in the factory's registry are permanent and queryable;
- future protocol versions preserve behavioral compatibility in both directions.

Every new version of pons.family can redeploy Snop and diff its execution trace against the original: gas usage, event ordering, revert conditions, state transitions. If the two match, the protocol's guarantees are intact.

---

# 10. The Role of Snop

Snop isn't a community token, a governance asset, or an investment. Its purpose is infrastructure.

As pons.family evolves, Snop becomes the mirrored benchmark used to validate new launch configurations, factory upgrades, liquidity systems, lockers, and deployment logic, checking step by step what Arcus already proved in the forward direction.

Just like engineers test new bridge designs against known structural principles, every future iteration of pons.family gets measured against the first reflection that proved the structure holds, from either side.

Learn more at [ponsfamily.com](https://ponsfamily.com).

---

> *A mirror doesn't change the bridge.*
>
> *It only confirms it holds, even in reverse.*

**Snop ($SNOP)**
*The mirror image of pons.family.*
*Protocol reference deployment. Test token. No holder utility.*
