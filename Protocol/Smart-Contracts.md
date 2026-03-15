# Smart Contracts

Aurora Protocol's on-chain infrastructure consists of **five core smart contracts** that together govern the complete lifecycle of a batch financing operation. All contracts are deployed on **Ethereum mainnet**, written in **Solidity ^0.8.20**, and built on top of **OpenZeppelin** standard libraries.

---

## Architecture Overview

```
                    ┌──────────────┐
                    │ BatchFactory │
                    └──────┬───────┘
                           │ deploys (minimal proxy clone)
              ┌────────────┼────────────┐
              ▼            ▼            ▼
      ┌──────────────┐ ┌───────────┐ ┌────────────┐
      │ AuroraRWA1155│ │PrimarySale│ │ EscrowVault│
      └──────────────┘ └───────────┘ └─────┬──────┘
                                           │
                                    ┌──────▼──────┐
                                    │  ClaimVault  │
                                    └─────────────┘
```

Each batch deployment creates a new set of linked contract instances. The **minimal proxy clone pattern** (EIP-1167) is used to minimize gas costs — each new instance delegates to a pre-deployed implementation contract rather than redeploying the full bytecode.

---

## Contract Specifications

### 1. BatchFactory

The factory contract is the single entry point for batch creation. It orchestrates the atomic deployment of all four child contracts for each new batch.

**Responsibilities:**
- Deploys minimal proxy clones of AuroraRWA1155, PrimarySale, EscrowVault, and ClaimVault
- Links the four contracts to each other during initialization
- Stores a registry of all deployed batches
- Enforces deployment-time parameters (funding target, token supply, milestone schedule, fee rate)

**Access:** Restricted to authorized deployers (Aurora Labs admin role).

### 2. AuroraRWA1155

The token contract implements the **ERC-1155** multi-token standard to represent fractional participation in a batch.

**Responsibilities:**
- Mints RWA tokens during the primary sale
- Tracks ownership and balances of fractional batch participation
- Supports burn operations for the claim process
- Stores batch-level metadata (URI, batch parameters)

**Design Rationale:** ERC-1155 was chosen over ERC-20 or ERC-721 for several reasons:
- A single contract can represent multiple token types (enabling future multi-tranche batches)
- Native batch transfer support reduces gas costs for portfolio operations
- Metadata extensibility through token URI standards

**Current State:** No secondary market trading is supported. Tokens are non-transferable in the current version (transfer restrictions enforced at the contract level). Secondary market functionality is planned for a future protocol upgrade.

### 3. PrimarySale

The sale contract manages the initial distribution of RWA tokens to participants.

**Responsibilities:**
- Accepts USDC deposits from participants
- Mints corresponding RWA tokens via AuroraRWA1155
- Enforces funding window (start time, end time)
- Enforces funding target (minimum and maximum raise)
- Forwards collected funds to the EscrowVault upon successful sale completion
- Returns funds to participants if the funding target is not met

**Denomination:** All primary sales are denominated in USDC (ERC-20 stablecoin).

### 4. EscrowVault

The escrow contract is the core fund management mechanism. It holds all batch capital and releases funds to the originator according to a predefined milestone schedule.

**Responsibilities:**
- Receives funds from the PrimarySale contract
- Manages a **7-state finite state machine** governing the batch lifecycle
- Releases milestone-based tranches to the originator upon authorized confirmation
- Handles failure transitions and participant refunds
- Deducts platform fees at the point of release

See [EscrowVault](EscrowVault.md) for the complete state machine specification.

### 5. ClaimVault

The claim contract manages the distribution of returns to token holders after batch completion.

**Responsibilities:**
- Receives return deposits (principal + yield) from the originator or EscrowVault
- Processes burn-to-claim redemptions: token holders burn their RWA tokens and receive proportional USDC
- Ensures exact accounting between total deposits and total claims
- Prevents double-claiming through burn mechanics (burned tokens cannot be reused)

See [Burn-to-Claim](Burn-to-Claim.md) for the full redemption mechanism.

---

## Security Model

### Role-Based Access Control

All contracts implement OpenZeppelin's **AccessControl** module with the following roles:

| Role | Scope | Assigned To |
|---|---|---|
| `DEFAULT_ADMIN_ROLE` | Full administrative control | Aurora Labs multisig (post-handover) |
| `DEPLOYER_ROLE` | Batch creation via BatchFactory | Aurora Labs deployer |
| `OPERATOR_ROLE` | Milestone confirmations, state transitions | Aurora Labs operator |
| `PAUSER_ROLE` | Emergency pause functionality | Aurora Labs admin |

### Post-Deployment Admin Handover

After initial deployment and configuration, the deployer account renounces its elevated privileges and transfers administrative control to a designated multisig wallet. This ensures that no single key can unilaterally modify contract state or access controls after the system is live.

### Upgrade Path

Current contracts are **non-upgradeable**. Each batch deployment is immutable once created. Protocol-level changes are introduced through new implementation contracts that future batches will clone from, while existing batches continue to operate under their original logic.

---

## Dependencies

| Library | Version | Usage |
|---|---|---|
| OpenZeppelin Contracts | ^5.0 | ERC-1155, AccessControl, ReentrancyGuard, Pausable |
| Solidity | ^0.8.20 | Language version |
| EIP-1167 | — | Minimal proxy clone pattern |

---

## Audit Status

Smart contracts have **not yet been audited** by a third-party security firm. A comprehensive audit is planned prior to mainnet launch of production batches. See [Risks](../Risks.md) for details on unaudited contract risk.
