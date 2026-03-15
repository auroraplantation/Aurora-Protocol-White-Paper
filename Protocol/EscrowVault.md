# EscrowVault

The EscrowVault is the core fund management contract in Aurora Protocol. It implements a **7-state finite state machine** that governs the complete lifecycle of batch capital — from initial deposit through milestone-based disbursement to final settlement or failure recovery.

---

## State Machine

```
                 ┌────────┐
                 │ Empty  │
                 └───┬────┘
                     │ PrimarySale deposits funds
                     ▼
                 ┌────────┐
           ┌─────│Funding │─────┐
           │     └───┬────┘     │
           │         │ target   │ target not met /
           │         │ reached  │ window expired
           │         ▼         │
           │     ┌────────┐     │
           │     │ Funded │     │
           │     └───┬────┘     │
           │         │ M1       │
           │         │ confirmed│
           │         ▼         │
           │   ┌───────────┐    │
           │   │Milestone 1│    │
           │   └─────┬─────┘    │
           │         │ M2       │
           │         │ confirmed│
           │         ▼         │
           │   ┌───────────┐    │
           │   │Milestone 2│    │
           │   └─────┬─────┘    │
           │         │ M3       │
           │         │ confirmed│
           │         ▼         │
           │   ┌───────────┐    │
           │   │Milestone 3│    │
           │   └───────────┘    │
           │                    │
           │     ┌────────┐     │
           └────►│ Failed │◄────┘
                 └────────┘
```

---

## State Definitions

| State | Description |
|---|---|
| **Empty** | Initial state. The vault has been deployed but contains no funds. |
| **Funding** | The PrimarySale is active. Funds are being deposited by participants. |
| **Funded** | The funding target has been reached. Sale is closed. Funds are locked and awaiting first milestone confirmation. |
| **Milestone 1** | First tranche has been released to the originator (e.g., planting phase funded). |
| **Milestone 2** | Second tranche released (e.g., growth/maintenance phase funded). |
| **Milestone 3** | Final tranche released. Batch lifecycle is complete. Returns are expected from the originator. |
| **Failed** | Terminal failure state. Triggered by funding shortfall, originator default, or operational failure. |

---

## State Transitions

### Valid Transitions

| From | To | Trigger |
|---|---|---|
| Empty | Funding | PrimarySale contract initiates the batch |
| Funding | Funded | Funding target reached within the sale window |
| Funding | Failed | Sale window expires without reaching target |
| Funded | Milestone 1 | Operator confirms M1 evidence |
| Funded | Failed | Originator defaults or batch is cancelled |
| Milestone 1 | Milestone 2 | Operator confirms M2 evidence |
| Milestone 1 | Failed | Originator defaults at M1 |
| Milestone 2 | Milestone 3 | Operator confirms M3 evidence |
| Milestone 2 | Failed | Originator defaults at M2 |

### Invalid Transitions

The following transitions are explicitly prohibited by the contract:

- **Empty → Failed** — A batch with no funds cannot fail; it simply remains uninitialized.
- **Milestone 3 → Failed** — Once all milestones are complete, the batch has succeeded. Failure is no longer a valid state.
- **Failed → any state** — Failed is a terminal state. No recovery or restart is possible.
- **Any backward transition** — States are strictly sequential. A batch cannot move from Milestone 2 back to Milestone 1.

---

## Fund Release Mechanics

Each milestone transition triggers a proportional fund release to the originator. The release schedule is defined at batch creation and encoded in the contract.

**Example 3-milestone schedule:**

| Milestone | Tranche | Cumulative Release |
|---|---|---|
| Milestone 1 | 30% | 30% |
| Milestone 2 | 35% | 65% |
| Milestone 3 | 35% | 100% |

At each release:
1. The platform fee (max 3%) is deducted from the tranche amount
2. The net amount is transferred to the originator's designated wallet
3. The state transition is recorded on-chain with a timestamp

---

## Failure Handling

When a batch transitions to the **Failed** state:

1. **Remaining funds** in the EscrowVault become available for participant withdrawal
2. **Each participant** can call a withdrawal function to reclaim their proportional share of the remaining balance
3. **Funds already released** in prior milestones are not recoverable through the smart contract — these are subject to off-chain recovery processes and originator staking penalties

The participant's recoverable amount in a failure scenario is:

```
recoverable = (participant_tokens / total_tokens) × remaining_vault_balance
```

---

## Access Control

| Action | Required Role |
|---|---|
| Initialize vault | BatchFactory (deployment only) |
| Transition: Funding → Funded | Automatic (triggered by PrimarySale) |
| Transition: Funded → Milestone N | `OPERATOR_ROLE` |
| Transition: Any → Failed | `OPERATOR_ROLE` |
| Withdraw (failure) | Any token holder |
| Emergency pause | `PAUSER_ROLE` |

---

## Security Properties

- **No manual fund extraction** — There is no administrative function to withdraw funds outside of the defined state machine logic.
- **Reentrancy protection** — All fund transfer functions are guarded by OpenZeppelin's `ReentrancyGuard`.
- **Single-direction state flow** — The state machine enforces strictly forward transitions, preventing replay or regression attacks.
- **Immutable schedule** — The milestone amounts and release percentages are set at deployment and cannot be modified after initialization.
