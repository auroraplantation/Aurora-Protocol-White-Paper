# Burn-to-Claim

The **Burn-to-Claim** mechanism is Aurora Protocol's returns distribution system. It is implemented through the **ClaimVault** contract and provides a deterministic, tamper-proof method for token holders to redeem their share of batch returns.

---

## Mechanism Overview

After a batch completes all three milestones, the originator deposits the agreed return amount (principal + yield) into the ClaimVault. Token holders then **burn** their ERC-1155 RWA tokens to claim their proportional share of the deposited funds.

The core principle is simple: **one token burned = one proportional claim settled**. Burning extinguishes the token permanently, ensuring that each claim can only be exercised once.

---

## Claim Flow

```
   Originator                 ClaimVault               Token Holder
       │                          │                          │
       │  deposit returns (USDC)  │                          │
       │─────────────────────────►│                          │
       │                          │                          │
       │                          │   burn RWA tokens        │
       │                          │◄─────────────────────────│
       │                          │                          │
       │                          │   transfer USDC          │
       │                          │─────────────────────────►│
       │                          │                          │
```

### Step-by-Step

1. **Return Deposit** — The originator transfers the full return amount (principal + yield) in USDC to the ClaimVault contract.

2. **Claim Initiation** — A token holder calls the `claim()` function on the ClaimVault, specifying the number of tokens to burn.

3. **Token Burn** — The ClaimVault calls `burn()` on the AuroraRWA1155 contract, permanently destroying the specified tokens from the holder's balance.

4. **USDC Transfer** — The ClaimVault calculates and transfers the proportional USDC amount to the holder's wallet.

---

## Claim Calculation

The amount each holder receives is calculated as:

```
claim_amount = (tokens_burned / total_token_supply) × total_vault_balance
```

Where:
- `tokens_burned` = number of RWA tokens the holder is burning in this transaction
- `total_token_supply` = total supply of RWA tokens for this batch at the time of the claim
- `total_vault_balance` = total USDC deposited in the ClaimVault for this batch

**Example:**
- Total token supply: 10,000
- Total vault balance: 105,000 USDC (100,000 principal + 5,000 yield)
- Holder burns 500 tokens
- Claim amount: (500 / 10,000) × 105,000 = **5,250 USDC**

---

## Design Properties

### No Double-Claiming

The burn mechanism inherently prevents double-claiming. Once tokens are burned, they are permanently removed from the holder's balance and from total supply. There is no way to re-mint or recover burned tokens.

### Partial Claims

Holders are not required to burn all their tokens at once. They can execute multiple partial claims over time. Each claim recalculates the proportional share based on the current remaining vault balance and remaining token supply.

### Atomic Execution

Each claim transaction is atomic — the burn and the USDC transfer occur in the same transaction. If either operation fails, the entire transaction reverts. There is no intermediate state where tokens are burned but funds are not transferred.

### No Expiry

There is no deadline to claim. Token holders can burn and claim at any time after the vault is funded. Unclaimed funds remain in the ClaimVault indefinitely.

---

## Edge Cases

| Scenario | Behavior |
|---|---|
| Holder tries to claim with zero tokens | Transaction reverts |
| Holder tries to burn more tokens than their balance | Transaction reverts |
| ClaimVault has zero balance | Transaction reverts (no funds to distribute) |
| Originator deposits partial returns | Holders receive proportional share of whatever is deposited |
| All tokens burned, residual dust in vault | Handled by integer rounding; negligible amounts may remain |

---

## Why Burn-to-Claim?

Alternative distribution mechanisms were considered and rejected:

| Approach | Issue |
|---|---|
| Airdrop (push-based) | Gas cost scales linearly with number of holders; sender pays all gas |
| Merkle claim (snapshot) | Requires off-chain snapshot generation; adds trust assumptions |
| Proportional streaming | Over-engineered for discrete batch settlements |
| **Burn-to-claim (pull-based)** | **Each holder pays their own gas; no snapshot needed; self-enforcing via token destruction** |

The burn-to-claim pattern is the most capital-efficient, trust-minimized, and gas-fair distribution method for Aurora's batch settlement model.
