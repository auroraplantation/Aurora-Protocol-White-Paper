# Business Model

Aurora Protocol generates revenue through a single, transparent fee mechanism: the **Platform Fee**. There are no hidden charges, token-based extraction mechanisms, or speculative revenue dependencies.

---

## Platform Fee

The Platform Fee is a percentage-based charge applied to the gross funds released from the EscrowVault at each milestone.

| Parameter | Value |
|---|---|
| Fee Type | Percentage of funds released |
| Maximum Rate | 3% |
| Typical Rate | 1.5%–3% (varies by batch) |
| Charged To | Originator (deducted from milestone disbursements) |
| Collection Point | At each milestone fund release |
| Recipient | Aurora Labs operating wallet |

### Key Properties

**Originator-borne:** The Platform Fee is deducted from the originator's disbursement, not from participant capital. Participants' return calculations are based on the originator's gross repayment obligation, which already accounts for the fee.

**Variable by batch:** The fee rate is set at batch creation and encoded in the smart contract. It can vary between batches based on factors such as batch size, originator risk profile, and relationship history. The maximum rate across all batches is capped at 3%.

**Milestone-aligned:** Fees are collected only when value is actually created — i.e., when a milestone is confirmed and funds are released. If a batch fails before a milestone, no fee is charged on unreleased tranches.

---

## Revenue Alignment

Aurora Protocol's business model is intentionally aligned with the interests of all participants:

**Alignment with participants:** Aurora Labs earns fees only when milestones are completed. If a batch fails, unreleased tranches generate no fee revenue. This creates a direct economic incentive for Aurora Labs to perform rigorous verification and select high-quality originators.

**Alignment with originators:** The fee is a known, fixed cost set before the batch begins. There are no variable spreads, hidden charges, or retroactive adjustments. Originators can calculate their exact cost of capital before committing.

**No token dependency:** Aurora Labs' core revenue model does not depend on the appreciation or trading volume of any token. Platform sustainability is grounded in real economic activity — agricultural financing operations generating fees from fund flows.

---

## What Aurora Protocol Does Not Charge

| Fee Type | Status |
|---|---|
| Participant entry/exit fee | None |
| Token transfer fee | None |
| Claim/burn fee | None |
| Subscription or access fee | None |
| Performance fee on yield | None |
| Originator onboarding fee | None |

---

## Future Revenue Considerations

As the protocol matures, additional revenue streams may be introduced. These are not currently implemented and will be subject to governance review and community input:

- **Secondary market fee** — A small transaction fee on secondary trading of RWA tokens, once secondary markets are enabled
- **Data and analytics services** — Premium data feeds or reporting for institutional participants
- **Verification-as-a-service** — Offering Aurora's verification infrastructure to third-party RWA protocols

Any new fee mechanism will be announced in advance and reflected in updated protocol documentation.
