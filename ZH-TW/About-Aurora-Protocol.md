# Aurora Protocol

**連結全球 DeFi 資金與實體農業資產**

---

我們相信，新興市場中高達 10 兆美元的農業融資缺口，是去中心化金融與實體經濟交匯處最具潛力的未開發機遇之一。東南亞數以百萬計的農業生產者無法獲得負擔得起的即時資金——並非因為他們不具備信用條件，而是因為傳統金融基礎設施從未被設計來觸及他們。

Aurora Protocol 是一個建構於 Ethereum 上的去中心化實體資產（RWA）融資平台。透過智能合約治理的批次融資、分割式參與代幣以及透明的託管生命週期，Aurora 將全球 DeFi 資金直接連結至農業生產者——移除中間人、降低成本，並釋放由實體生產性資產支撐的收益。

Aurora 上的每一個批次都代表一筆真實的農業融資操作：可驗證的生產者、明確的里程碑、以及由鏈上合約強制執行的確定性資金流向。參與者透過購買 ERC-1155 分割式代幣來資助特定批次，並在批次成功完成後透過銷毀領取（Burn-to-Claim）機制取回收益。

Aurora Protocol 不是借貸協議、收益聚合器或投機工具。它是一種全新鏈上實體資產類別的基礎設施——根植於糧食生產、供應鏈物流和新興市場成長的經濟邏輯之中。

---

## 核心原則

**預設透明** — 所有資金流向、狀態轉換和里程碑事件均記錄於鏈上，所有參與者均可檢視。

**真實資產，真實收益** — 收益來自實際的農業融資操作，而非代幣增發或反身性激勵循環。

**確定性執行** — 智能合約強制執行批次生命週期，無手動覆寫機制。資金僅在預設條件滿足時流動。

**無許可參與** — 任何擁有 Web3 錢包的人均可參與批次融資，不受地理位置或機構身份限制。

**風險隔離** — 每個批次均為獨立的經濟單元，單一批次的表現不影響其他批次。

---

## 運作方式概覽

1. **批次建立** — 農業發起人提交融資申請。Aurora Labs 驗證其底層操作並透過 BatchFactory 合約部署新批次。

2. **初級銷售** — DeFi 參與者購買 ERC-1155 分割式 RWA 代幣，代表其在該批次中的份額。所有資金流入專屬 EscrowVault。

3. **里程碑執行** — 隨著實際里程碑（播種、生長、收穫）獲得驗證並在鏈上確認，資金按階段釋放給發起人。

4. **收益分配** — 批次完成後，收益存入 ClaimVault。代幣持有者銷毀其 RWA 代幣以領取按比例分配的份額。

---

## 快速導覽

| 章節 | 說明 |
|---|---|
| [運作方式](Protocol/How-It-Works.md) | 完整批次生命週期 |
| [智能合約](Protocol/Smart-Contracts.md) | 五合約架構 |
| [EscrowVault](Protocol/EscrowVault.md) | 七狀態託管狀態機 |
| [銷毀領取](Protocol/Burn-to-Claim.md) | ClaimVault 贖回機制 |
| [驗證架構](Protocol/Verification.md) | 五層驗證體系 |
| [單位經濟](Economics/Unit-Economics.md) | 批次層級財務模型 |
| [商業模式](Economics/Business-Model.md) | 平台費用結構 |
| [發起人擔保](Economics/Originator-Security.md) | $AUR 質押門檻 |
| [積分計畫](Economics/Points-Program.md) | Aurora 積分與空投權重 |
| [市場機會](Market/Market-Opportunity.md) | 東南亞農業融資 |
| [為何選擇 Aurora](Market/Why-Aurora.md) | 競爭定位 |
| [發展路線](Roadmap.md) | 開發里程碑 |
| [團隊](Team.md) | 核心貢獻者 |
| [風險揭露](Risks.md) | 風險說明 |
| [法律與合規](Legal-and-Compliance.md) | 監管框架 |
| [免責聲明](Disclaimers.md) | 法律免責 |

---

**官方網站：** [auroraworlds.com](https://auroraworlds.com)
**聯絡信箱：** [support@auroraworlds.com](mailto:support@auroraworlds.com)
**開發團隊：** Aurora Labs
**營運主體：** Aurora Digital Labs Limited（香港）
