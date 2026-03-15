# Risk Disclosures

Participation in Aurora Protocol involves significant risks. This section provides a comprehensive overview of the risks that participants should understand before purchasing RWA tokens or engaging with the protocol. This is not an exhaustive list, and additional risks may emerge as the protocol evolves.

---

## Smart Contract Risk

Aurora Protocol's smart contracts have **not yet been audited** by a third-party security firm. Unaudited smart contracts may contain bugs, vulnerabilities, or logic errors that could result in loss of funds. Even after audit, no smart contract can be guaranteed to be free of vulnerabilities.

**Specific risks include:**
- Undiscovered bugs in escrow, sale, or claim logic
- Reentrancy or access control vulnerabilities
- Unforeseen interactions between linked contracts
- Dependency on OpenZeppelin library correctness

**Mitigation:** A comprehensive third-party audit is planned prior to production batch deployment. Contracts are built on widely-used, battle-tested OpenZeppelin standards.

---

## Originator Default Risk

The originator may fail to repay the agreed return amount. Default may result from:

- Crop failure (disease, pests, drought, flooding)
- Market price decline below the originator's cost basis
- Operational mismanagement
- Fraud or misrepresentation
- Force majeure events (natural disasters, political instability)

**Consequence:** Partial or total loss of participant capital. Funds already disbursed in prior milestones are not recoverable through the smart contract.

**Mitigation:** 5-layer verification architecture, milestone-based disbursement, originator $AUR staking (when activated), and off-chain legal agreements.

---

## Agricultural and Climate Risk

Agricultural operations are inherently exposed to environmental and biological risks:

- Weather events (typhoons, drought, excessive rainfall)
- Pest and disease outbreaks
- Soil degradation
- Climate change impacts on growing seasons and yields

These risks can cause partial or total crop failure, which directly impacts the originator's ability to repay.

---

## Market and Commodity Price Risk

Agricultural returns depend on the sale price of harvested commodities. If market prices decline significantly between the time of financing and the time of sale, the originator may generate insufficient revenue to cover repayment obligations.

---

## Stablecoin Risk

All Aurora Protocol transactions are denominated in **USDC**. USDC is issued by Circle and is subject to:

- **Issuer risk** — Circle could face regulatory action, insolvency, or operational failure
- **Redemption risk** — USDC may trade below par during stress events
- **Freeze risk** — Circle has the ability to freeze USDC held in specific addresses pursuant to law enforcement requests or regulatory orders
- **Smart contract risk** — The USDC contract itself could have vulnerabilities

Aurora Protocol does not control or guarantee the stability or availability of USDC.

---

## Liquidity Risk

RWA tokens are currently **non-transferable**. There is no secondary market for trading RWA tokens. Participants cannot exit their position before the batch lifecycle concludes. Secondary market functionality is planned but not guaranteed.

Even after secondary markets are enabled, RWA tokens may have limited liquidity due to small batch sizes, limited market participants, or lack of market maker support.

---

## Regulatory and Legal Risk

- Regulatory frameworks for digital assets, tokenized securities, and DeFi protocols are evolving rapidly and vary by jurisdiction
- Aurora Protocol may be subject to regulatory actions in Hong Kong or other jurisdictions
- Changes in law or regulation could restrict protocol operations, require participant identification, or prohibit participation from certain jurisdictions
- The classification of RWA tokens as securities, utility tokens, or other instruments is not definitively settled in all jurisdictions

---

## Operational Risk

Aurora Protocol is currently operated by **Aurora Labs**, a small team. Operational risks include:

- Key person dependency
- Operational errors in verification or milestone confirmation
- Data entry errors (current data entry is manual)
- Communication failures with originators
- Infrastructure downtime or frontend unavailability

---

## Ethereum Network Risk

Aurora Protocol is deployed exclusively on Ethereum mainnet. Risks include:

- Network congestion causing high gas fees or delayed transactions
- Ethereum protocol changes that affect contract behavior
- MEV (maximal extractable value) attacks on transactions
- Potential chain reorganizations or consensus failures

---

## Concentration Risk

During early operations, Aurora Protocol may rely on a small number of originators and geographic regions. Poor performance by a single originator or adverse conditions in a single market could disproportionately impact platform performance and reputation.

---

## $AUR Token Risk

The $AUR governance token has not yet been issued. Risks related to the future $AUR token include:

- The token may never be issued
- Token characteristics, supply, and distribution may change from current descriptions
- $AUR may have no liquid market or may trade significantly below expectations
- Regulatory developments may restrict $AUR issuance or distribution

---

## No Insurance or Guarantee

Aurora Protocol does not provide deposit insurance, principal guarantees, or any form of return guarantee. Participation in any batch may result in partial or total loss of invested capital.

---

## General Disclaimer

This risk disclosure section is provided for informational purposes and does not constitute legal, financial, or investment advice. Participants should conduct their own due diligence and consult qualified advisors before participating in Aurora Protocol. See [Disclaimers](Disclaimers.md) for full legal disclaimers.
