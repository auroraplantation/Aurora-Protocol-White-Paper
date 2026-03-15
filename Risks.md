# Risks

> **Participation in Aurora Protocol involves significant risks. Prospective participants should carefully consider the following risk factors before engaging with the platform.**

---

## Risk Matrix

| Category | Risk | Severity | Likelihood | Mitigation |
|----------|------|:--------:|:----------:|------------|
| **Smart Contract** | Undiscovered vulnerabilities in protocol contracts | High | Low–Medium | Third-party audit (planned), OpenZeppelin standards, minimal proxy isolation |
| **Smart Contract** | Dependency on OpenZeppelin library security | Medium | Low | Use of battle-tested, widely-audited library versions |
| **Originator** | Default on repayment obligations | High | Medium | Originator staking, 5-layer verification, milestone gating |
| **Originator** | Fraudulent batch submissions | High | Low | Physical inspection, identity verification, staking collateral |
| **Agricultural** | Crop failure due to weather, disease, or pests | High | Medium | Diversification across crops, regions, and seasons; milestone-based release |
| **Agricultural** | Market price volatility for harvested crops | Medium | Medium | Conservative yield projections, Originator pricing agreements |
| **Market** | Insufficient investor demand for batch subscriptions | Medium | Medium | Points Program incentives, community growth, competitive yields |
| **Market** | Illiquidity of RWA tokens (no secondary market) | Medium | High | Secondary market planned; tokens redeemable at maturity via burn-to-claim |
| **Regulatory** | Changes in Hong Kong digital asset regulations | Medium | Low–Medium | Ongoing legal monitoring, Cap. 617 compliance framework |
| **Regulatory** | Classification of RWA tokens as regulated securities | High | Medium | Legal structuring as participation tokens, not equity or debt instruments |
| **Stablecoin** | USDC issuer (Circle) freeze or blacklist of protocol addresses | High | Low | Monitoring issuer policies, contingency planning |
| **Stablecoin** | USDC de-peg from USD | Medium | Low | Established USDC track record; no mitigation against systemic de-peg events |
| **Operational** | Manual verification errors or delays | Medium | Medium | Standardized verification checklists, planned automation |
| **Operational** | Key-person dependency on small core team | Medium | Medium | Documentation, knowledge sharing, planned team expansion |
| **Network** | Ethereum gas cost spikes | Low | Medium | EIP-1167 proxy pattern minimizes deployment costs; L2 migration planned |
| **Network** | Ethereum network congestion or downtime | Low | Low | Non-time-critical settlement design; milestone deadlines accommodate delays |

---

## Risk Categories Explained

### Smart Contract Risk

Aurora Protocol's contracts have not yet undergone a formal third-party security audit. While the architecture follows industry best practices — including OpenZeppelin standards, role-based access control, and minimal proxy isolation — undiscovered vulnerabilities may exist. A comprehensive audit is planned prior to mainnet launch of live financing batches.

### Originator and Agricultural Risk

The protocol finances real-world agricultural activities subject to natural, operational, and market risks. Crop failures, supply chain disruptions, and originator default are inherent to this asset class. The milestone-gated disbursement model and originator staking mechanism are designed to reduce, but cannot eliminate, these risks.

### Regulatory Risk

The regulatory landscape for digital assets and tokenized real-world assets is evolving globally. Changes in Hong Kong regulations or in jurisdictions where investors or originators are located could impact the protocol's operations, fee structures, or the legal status of RWA tokens.

### Stablecoin Risk

All protocol settlements are denominated in `USDC`. As a centralized stablecoin, USDC is subject to issuer risk — including the possibility that Circle may freeze or blacklist specific addresses. A de-peg event, though historically brief, could affect the value of funds in transit.

### Liquidity Risk

RWA tokens currently have no secondary market. Investors should consider their investment illiquid until the batch reaches maturity and burn-to-claim redemption becomes available. A secondary trading venue is planned but not yet operational.

---

> *This list is not exhaustive. Additional risks may emerge as the protocol, market, and regulatory environment evolve. Participants should conduct their own due diligence and consult professional advisors before making any investment decisions.*

---

> **Next**: [Legal and Compliance →](Legal-and-Compliance.md)
