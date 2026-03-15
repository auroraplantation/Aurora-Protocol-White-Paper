# Originator Security

> **Aurora Protocol requires originators to stake collateral as a commitment mechanism, aligning their incentives with investor protection and batch performance.**

---

## Overview

In any RWA financing protocol, the risk of originator default or misconduct is a primary concern. Aurora Protocol mitigates this risk through a mandatory staking requirement: originators must lock collateral before their batch can proceed to primary sale.

This mechanism serves as both a financial commitment and a behavioral incentive — originators with capital at stake are more likely to fulfill their obligations and deliver on milestones.

---

## Staking Mechanism

### How It Works

1. **Pre-Batch Requirement**: Before a batch is approved for primary sale, the Originator must deposit a staking amount into the protocol
2. **Lock Period**: The stake remains locked for the entire duration of the batch lifecycle — from funding through final repayment
3. **Release on Completion**: Upon successful completion of all milestones and full repayment, the stake is returned to the Originator
4. **Forfeiture on Failure**: If the batch enters a **Failed** state, part or all of the stake may be forfeited and distributed to affected investors as partial compensation

---

## Staking Parameters

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Staking Token** | `$AUR` (planned) | Governance token — acts as entry gate |
| **Minimum Stake** | TBD | To be determined based on batch size tiers |
| **Lock Duration** | Full batch lifecycle | Release upon successful repayment |
| **Forfeiture Trigger** | Batch enters Failed state | Partial or full forfeiture |
| **Forfeiture Distribution** | Pro-rata to affected investors | Proportional to token holdings |

> *Note: The `$AUR` governance token has not yet been issued. During the pre-token phase, staking requirements may be fulfilled through alternative collateral arrangements as determined by the platform.*

---

## Incentive Alignment

| Stakeholder | Incentive |
|-------------|-----------|
| **Originator** | Staking creates direct financial exposure to batch success — discourages negligence and fraud |
| **Investor** | Staking provides a first-loss buffer — partial protection against originator default |
| **Platform** | Staking raises the quality bar for originators — only committed producers participate |

---

## Risk Mitigation Matrix

| Risk | Mitigation via Staking |
|------|------------------------|
| **Originator abandons batch** | Forfeited stake compensates investors |
| **Milestone fraud** | Staked capital at risk incentivizes honest reporting |
| **Repeated bad actors** | Forfeiture history disqualifies originators from future batches |
| **Under-collateralized batch** | Minimum stake requirements scaled to batch size |

---

## Future Enhancements

As the `$AUR` token ecosystem matures, the staking mechanism will evolve:

| Enhancement | Description |
|-------------|-------------|
| **Tiered Staking** | Higher-tier originators (based on track record) may qualify for reduced staking requirements |
| **Staking Rewards** | Successful originators may earn additional `$AUR` rewards for on-time repayment |
| **Delegated Staking** | Third parties may stake on behalf of originators, expanding access for smaller producers |
| **Slashing Conditions** | Formalized on-chain slashing rules for specific failure scenarios |

---

> **Next**: [Points Program →](Points-Program.md)
