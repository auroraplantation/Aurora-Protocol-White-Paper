# How It Works

Aurora Protocol operates through a **batch-based financing lifecycle** that connects DeFi capital providers with agricultural producers in Southeast Asia. Each batch represents a single, self-contained financing operation with a defined timeline, asset type, and return profile.

---

## The Batch Lifecycle

### Phase 1 — Origination

An agricultural originator — typically a cooperative, aggregator, or farm operator — submits a financing request to Aurora Labs. The request specifies:

- Crop type, geography, and production timeline
- Financing amount required (denominated in USDC)
- Expected return and repayment schedule
- Milestone structure (typically aligned with planting, growth, and harvest cycles)

Aurora Labs performs due diligence through the [5-layer verification architecture](Verification.md), assessing the originator's track record, operational capacity, and the viability of the underlying agricultural operation.

### Phase 2 — Batch Deployment

Upon approval, Aurora Labs deploys a new batch on-chain via the **BatchFactory** contract. This single transaction atomically creates:

- A new **AuroraRWA1155** token contract representing fractional participation in the batch
- A linked **PrimarySale** contract for token distribution
- A dedicated **EscrowVault** to hold and release funds according to the milestone schedule
- A linked **ClaimVault** for returns distribution upon completion

Each batch is a completely independent on-chain entity. There is no cross-collateralization or shared state between batches.

### Phase 3 — Primary Sale

The batch enters a funding window during which DeFi participants can purchase ERC-1155 RWA tokens through the PrimarySale contract. Key mechanics:

- **Denomination:** All transactions are in USDC
- **Fractional Access:** Each token represents an equal fractional share of the batch
- **Fixed Price:** Token price is set at batch creation and does not change during the sale
- **Funding Target:** The batch has a defined target amount; the sale closes when the target is reached or the window expires

If the funding target is not met within the window, the batch transitions to a **Failed** state and all funds are returned to participants via the EscrowVault.

### Phase 4 — Milestone Execution

Once fully funded, the EscrowVault transitions through a series of milestone states:

```
Funded → Milestone 1 → Milestone 2 → Milestone 3
```

At each milestone:

1. The originator submits evidence of milestone completion (e.g., planting confirmation, growth inspection, harvest documentation)
2. Aurora Labs verifies the evidence through its verification process
3. Upon confirmation, the smart contract releases the corresponding tranche of funds to the originator

This staged release mechanism ensures that capital is disbursed only as real-world progress is demonstrated. See [EscrowVault](EscrowVault.md) for the full state machine specification.

### Phase 5 — Returns Distribution (Burn-to-Claim)

Upon successful completion of all milestones:

1. The originator deposits the agreed return amount (principal + yield) into the **ClaimVault**
2. The EscrowVault reaches its terminal state (Milestone 3 complete)
3. RWA token holders burn their tokens through the ClaimVault to claim their proportional share of the returns

The burn-to-claim mechanism ensures a clean, deterministic settlement: one token equals one claim, and burning it extinguishes the obligation. See [Burn-to-Claim](Burn-to-Claim.md) for details.

---

## Failure Handling

If a batch fails at any stage after funding — due to crop failure, originator default, or force majeure — the EscrowVault transitions to a **Failed** state. In this scenario:

- Any unreleased funds remaining in the EscrowVault are made available for participant withdrawal
- Funds already disbursed to the originator in prior milestones are subject to off-chain recovery processes
- The originator's staked $AUR collateral (see [Originator Security](../Economics/Originator-Security.md)) may be slashed as a partial loss mitigation mechanism

Aurora Protocol does not guarantee principal return. Each batch carries independent risk, and participants should evaluate each batch on its own merits.

---

## Participant Roles

| Role | Description |
|---|---|
| **DeFi Participant** | Purchases RWA tokens to fund batches; earns yield upon successful completion |
| **Originator** | Agricultural producer or aggregator seeking financing; must pass verification and stake $AUR |
| **Aurora Labs** | Platform operator; deploys batches, manages verification, operates the frontend |
| **Smart Contracts** | Autonomous on-chain enforcement of fund flows, state transitions, and claims |

---

## Key Properties

- **Non-custodial:** Aurora Labs never holds participant funds. All capital sits in smart contracts.
- **Deterministic:** Fund releases follow predefined rules. No manual override of contract state.
- **Isolated:** Each batch is economically independent. One batch's failure does not cascade to others.
- **Transparent:** All state transitions, fund movements, and claims are visible on Ethereum.
