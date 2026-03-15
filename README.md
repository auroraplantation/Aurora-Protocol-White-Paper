# About Aurora Protocol

> **Connecting global DeFi capital with real-world agricultural producers through trustless, transparent, and programmable financing.**

---

## Background

Across Southeast Asia, millions of smallholder farmers and agricultural cooperatives face a persistent financing gap. Traditional banks impose prohibitive collateral requirements, lengthy approval cycles, and opaque fee structures that exclude the majority of rural producers from formal credit markets. The World Bank estimates that the global agricultural financing gap exceeds **$170 billion annually**, with Southeast Asia accounting for a disproportionate share.

At the same time, decentralized finance (DeFi) has unlocked trillions of dollars in on-chain liquidity — capital that is programmable, permissionless, and globally accessible. Yet this capital remains largely disconnected from real-world productive assets, cycling instead through speculative loops with limited economic impact.

**The opportunity is clear**: bridge verified real-world agricultural assets to DeFi capital markets through a protocol that is transparent, auditable, and governed by smart contracts rather than intermediaries.

---

## About

Aurora Protocol is a decentralized Real-World Asset (RWA) financing platform built on Ethereum. It enables agricultural producers — referred to as **Originators** — to tokenize verified crop financing batches into fractional ERC-1155 participation tokens, which global investors can purchase using `USDC`.

The protocol governs the full lifecycle of each financing batch through a five-contract smart contract architecture:

- **Batch creation and token minting** via `BatchFactory` and `AuroraRWA1155`
- **Primary market subscription** via `PrimarySale`
- **Milestone-based fund disbursement** via `EscrowVault`
- **Investor redemption** via `ClaimVault` using a burn-to-claim mechanism

Every transaction — from subscription to final payout — is executed on-chain, eliminating the need for traditional custodians or manual settlement processes.

---

## Ecosystem Structure

The Aurora Protocol ecosystem is organized around three interdependent pillars:

| Pillar | Description | Learn More |
|--------|-------------|------------|
| **Protocol** | The smart contract infrastructure that governs batch creation, escrow, milestone disbursement, and investor claims. | [How It Works](Protocol/How-It-Works.md) |
| **Economics** | The incentive and revenue model that aligns originators, investors, and the platform through transparent fee structures and a points-based loyalty program. | [Unit Economics](Economics/Unit-Economics.md) |
| **Market** | The addressable opportunity in Southeast Asian agricultural financing and Aurora's competitive positioning within the RWA landscape. | [Market Opportunity](Market/Market-Opportunity.md) |

---

## Key Facts

| Parameter | Detail |
|-----------|--------|
| **Blockchain** | Ethereum Mainnet |
| **Token Standard** | ERC-1155 (Fractional Participation Tokens) |
| **Settlement Currency** | `USDC` |
| **Smart Contract Framework** | OpenZeppelin, Solidity ^0.8.20 |
| **Deployment Pattern** | Minimal Proxy Clone (EIP-1167) |
| **Platform Fee** | ≤ 3% per batch |
| **Entity** | Aurora Digital Labs Limited (Hong Kong) |
| **Website** | [auroraworlds.com](https://auroraworlds.com) |
| **Contact** | support@auroraworlds.com |

---

> *This whitepaper is for informational purposes only and does not constitute financial, legal, or investment advice. Please refer to the [Disclaimers](Disclaimers.md) section for full terms.*

---

## Table of Contents

### Protocol

- [How It Works](Protocol/How-It-Works.md)
- [Smart Contracts](Protocol/Smart-Contracts.md)
- [EscrowVault](Protocol/EscrowVault.md)
- [Burn-to-Claim](Protocol/Burn-to-Claim.md)
- [Verification](Protocol/Verification.md)

### Economics

- [Unit Economics](Economics/Unit-Economics.md)
- [Business Model](Economics/Business-Model.md)
- [Originator Security](Economics/Originator-Security.md)
- [Points Program](Economics/Points-Program.md)

### Market

- [Market Opportunity](Market/Market-Opportunity.md)
- [Why Aurora](Market/Why-Aurora.md)

### Additional

- [Roadmap](Roadmap.md)
- [Team](Team.md)
- [Risks](Risks.md)
- [Legal and Compliance](Legal-and-Compliance.md)
- [Disclaimers](Disclaimers.md)
