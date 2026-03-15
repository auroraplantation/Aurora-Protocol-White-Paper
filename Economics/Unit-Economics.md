# Unit Economics

This section describes the economic structure of a single Aurora Protocol batch — the fundamental unit of financing on the platform. Understanding batch-level economics is essential for both DeFi participants evaluating investment opportunities and originators structuring financing requests.

---

## Batch as Economic Unit

Each batch on Aurora Protocol is a self-contained financing operation with its own:

- Funding target (denominated in USDC)
- Token supply and price
- Milestone schedule and release percentages
- Fee structure
- Expected return profile
- Independent risk profile

There is no portfolio-level pooling, cross-subsidization, or shared liability between batches. Each batch succeeds or fails on its own merits.

---

## Illustrative Batch Structure

The following example illustrates the economics of a typical agricultural financing batch:

### Batch Parameters

| Parameter | Value |
|---|---|
| Crop Type | Thai Jasmine Rice |
| Financing Amount | 100,000 USDC |
| Token Supply | 10,000 RWA tokens |
| Token Price | 10 USDC |
| Batch Duration | 6 months (1 crop cycle) |
| Expected Gross Return | 12% annualized (6% for the 6-month cycle) |
| Platform Fee | 2.5% (of principal, deducted at milestone release) |

### Fund Flow

```
DeFi Participants
       │
       │ 100,000 USDC
       ▼
   PrimarySale
       │
       │ 100,000 USDC
       ▼
   EscrowVault ──────── Platform Fee: 2,500 USDC ──────► Aurora Labs
       │
       │ 97,500 USDC (net to originator across 3 milestones)
       ▼
   Originator
       │
       │ 106,000 USDC (principal + yield)
       ▼
   ClaimVault
       │
       │ 106,000 USDC (distributed via burn-to-claim)
       ▼
DeFi Participants
```

### Participant Returns

| Metric | Value |
|---|---|
| Investment per token | 10 USDC |
| Return per token (if successful) | 10.60 USDC |
| Net yield per token | 0.60 USDC (6% for 6-month cycle) |
| Annualized yield (gross) | ~12% |
| Platform fee borne by | Originator (deducted from disbursement) |

### Originator Economics

| Metric | Value |
|---|---|
| Financing received (net of fee) | 97,500 USDC |
| Repayment obligation | 106,000 USDC |
| Effective cost of capital | ~8.7% for 6 months (~17.4% annualized) |
| Platform fee paid | 2,500 USDC |

---

## Fee Deduction Mechanics

The platform fee is deducted from each milestone tranche as funds are released from the EscrowVault. This means the fee is distributed across the batch lifecycle rather than front-loaded.

**Example with 3 milestones (30/35/35 split):**

| Milestone | Gross Release | Fee (2.5%) | Net to Originator |
|---|---|---|---|
| Milestone 1 | 30,000 USDC | 750 USDC | 29,250 USDC |
| Milestone 2 | 35,000 USDC | 875 USDC | 34,125 USDC |
| Milestone 3 | 35,000 USDC | 875 USDC | 34,125 USDC |
| **Total** | **100,000 USDC** | **2,500 USDC** | **97,500 USDC** |

---

## Yield Disclaimer

Projected yields are **estimates based on the originator's expected crop economics** and are not guaranteed. Actual returns depend on:

- Crop performance and harvest quality
- Commodity market prices at the time of sale
- Originator's operational execution
- External factors (weather, logistics, policy changes)
- Originator's ability and willingness to repay

A batch may return less than projected, return only the principal, or result in partial or total loss of capital. See [Risks](../Risks.md) for full risk disclosures.

---

## Comparison with Traditional Agricultural Finance

| Dimension | Traditional | Aurora Protocol |
|---|---|---|
| Minimum investment | $50,000–$500,000+ | As low as 1 token (~$10 equivalent) |
| Geographic access | Local banks, regional DFIs | Global, permissionless |
| Transparency | Quarterly reports, limited visibility | Real-time on-chain state |
| Settlement | 30–90 day manual processes | Deterministic smart contract execution |
| Intermediaries | Multiple (banks, brokers, agents) | Direct participant-to-originator via smart contract |
| Liquidity | Illiquid, fixed-term commitments | Currently illiquid; secondary market planned |
