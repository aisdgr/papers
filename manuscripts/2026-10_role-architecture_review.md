# Role Architecture — 核心思維與架構調整建議

> 對象：`2026-10_role-architecture.md`（概念稿）
> 範圍：只處理核心論點、概念模型與章節架構；不含文字潤飾、引用格式與文獻補齊細節。

---

## 0. 總評

稿件有兩條論點同時在跑，且彼此爭奪主軸：

| 論點線                                                                   | 出現位置                                | 問題                                                                       |
| ------------------------------------------------------------------------ | --------------------------------------- | -------------------------------------------------------------------------- |
| **A. Role Drift**：角色意義跨模型／流程重用時被重新推論而漂移            | 標題、Abstract、§3.6、§5.8、P8–P9、結論 | 是本文真正的新貢獻，但在正文中只占一節加一個 failure mode                  |
| **B. Role Validity**：一次行動是否由負責、有權、有能力、可延續的角色執行 | §2、§4、§5 大部分、§6 例子              | 與 Continuation Readiness、DA/DR 高度重疊，且 B 本身不需要「持久化」也成立 |

**建議：以 A 為唯一主軸，B 降為 A 的檢測手段。** 五項 validity 條件改寫為「Role State 是否忠於 Role Definition 的檢查維度」，而非獨立的 accountability 理論。否則審稿者會判定本文是 Continuation Readiness 的延伸，而非獨立貢獻。

主軸一句話建議改為（直接套用 Engineering Determinacy 的 model-independent determinacy）：

> **已確立的角色意義，不應因消費它的模型、流程或執行次數改變而改變。**

---

## 1. 核心論點調整

### 1.1 問題定義：從「表示不足」改為「重新推論」

§2 目前論證「職稱／權限／流程 lane／persona 不足以建立 accountability」，這是 B 線的論證。A 線應該論證的是：

- 每一種既有表示**只持久化角色的一個維度**（職稱→身分、RBAC→permission、lane→活動、persona→行為傾向、RACI→責任類別）；
- 其餘維度在每次使用時**由模型或人重新推論**；
- 重新推論在確定性執行者（傳統軟體、受訓人員）下相對穩定，在 LLM 下是機率性的 → 同一標籤產生不同 Role State。

這樣 §2 就直接導出 Role Drift，而不是導出「accountability 缺口」。

### 1.2 新穎性定位：必須正面處理 MAS 組織模型

目前 §11 只泛稱「需比對 role theory、RBAC、MAS…」。實際上有幾個前作與本文的 Role Definition 結構**非常接近**，審稿時必然被點名：

| 前作                                                       | 已具備                                                         | 本文需主張的差異                                                    |
| ---------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------- |
| Gaia（Wooldridge et al., 2000）                            | Role = responsibilities + permissions + activities + protocols | Gaia 假設 agent 以確定性方式實作 role；未處理機率性重建與跨模型漂移 |
| MOISE+ / OperA                                             | 角色、mission、norm、組織結構                                  | 同上；且無版本／binding／override 治理                              |
| NIST RBAC（含 SSD/DSD）                                    | 角色階層、static/dynamic separation of duties                  | SoD 已是成熟機制，本文 §5.6 Role Collision 不能當成新貢獻           |
| Agent 規格（A2A AgentCard、CrewAI role/goal/backstory 等） | 可重用的 agent 角色描述                                        | 屬 persona/能力宣告，無 authority、責任、版本漂移治理               |

建議明確宣告：**貢獻不在角色結構本身，而在「LLM 條件下角色意義的持久化、綁定與漂移控制」**。§11 第一段已有此意，應提前到 §1 作為定位聲明。

另：避免使用 **Role Engineering** 作為關鍵字，此詞在 RBAC 領域已有固定意義（Coyne, 1996），會造成誤讀。

### 1.3 與既有研究體系的術語衝突

| 衝突點                         | 現稿用法                                                                 | 既有 canonical 用法                                                                | 建議                                                                                                                                                  |
| ------------------------------ | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Authority**                  | 「可決定、核准、變更、拒絕或引發什麼」— 接近 decision right / permission | BRA：Authority = Policy (MUST) + Constraint (MUST NOT)，**不是** authorization     | 必須擇一。若保留 BRA 定義，則 Role Definition 中的 Authority 與 Constraints 應合併為「bound rule set」，另立 **Decision Right** 承載「可決定什麼」    |
| **Scope**                      | 單一 Applicable Scope                                                    | Visible Scope ≠ Artifact Scope                                                     | Role Definition 至少拆為 Visible Scope（可讀／可取證）與 Artifact Scope（可修改）；Behavior Space = Artifact Scope × Authority 可直接作為角色行為邊界 |
| **Responsibility Vacancy**     | §5.5 自行命名                                                            | DR-V（Decision Vacancy：Never Authorized / Lost in Transition / Implicit Handoff） | 直接引用 DR-V，並說明 Role Architecture 提供 DR-V 的角色層成因                                                                                        |
| **Authority Drift / 越權決策** | §5.8、§6.3 caching 例子                                                  | DR-O（Over Decision）                                                              | §6.3 的 Implementation Agent 選 caching strategy 是典型 DR-O，應明確對應                                                                              |
| **Role State**                 | 本文定義                                                                 | Continuation Readiness 已定義                                                      | 需說明本文定義是否擴充／修訂原定義，並保持欄位一致                                                                                                    |

---

## 2. 概念模型調整

### 2.1 Role Definition 元素分層

13 個元素平鋪，未區分核心與延伸，也無法支撐「minimum completeness」。建議分四層：

| 層                             | 元素                                                                                       | 性質                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **L1 Identity**                | Identity、Version、Description                                                             | 可解析性；漂移比較的錨點（對應 Anchor Architecture） |
| **L2 Semantic Core**           | Viewpoints、Work Definition、Responsibilities                                              | 最容易被機率性重建的部分；**漂移主要發生層**         |
| **L3 Governance Boundary**     | Authority（BRA rule set）、Decision Right、Visible / Artifact Scope、Required Capabilities | 綁定時的單調性檢查對象                               |
| **L4 Interface & Interaction** | Input/Output Contract、Interaction Rules、Escalation、Evidence Requirements                | 角色間組合與驗證                                     |

Minimum completeness = L1 + L2 + L3 必要；L4 依流程而定。

### 2.2 Binding 規則：補上單調性，並指出 Responsibility 的反例

`R = Bind(Dᵥ, A, C, O)` 目前只說 override 可「narrow」不可「silently expand」。這對 Scope 與 Authority 成立，**對 Responsibility 不成立**：

- Scope、Decision Right、Artifact Scope：binding 只可縮小（⊆）；
- Constraint（MUST NOT）：binding 只可增加；
- **Responsibility：縮小即產生 vacancy**。縮小責任必須同時宣告承接角色，否則等同 DR-V。

這是本文可以提出的一個非顯然論點，建議寫成明確的 binding invariant，而非僅一句「may narrow」。

### 2.3 Role Drift 操作化

現稿「effective meaning diverges」不可觀測。建議：

1. **以 locus 區分漂移類型**（取代 §3.6 的「across models/workflows/stages…」清單）：

| Locus                | 定義                               | 檢測時點             |
| -------------------- | ---------------------------------- | -------------------- |
| **Definition Drift** | 同一 identifier 下內容改變而未升版 | 版本比對             |
| **Binding Drift**    | 實例化時未宣告的擴張、替換或省略   | 綁定前 conformance   |
| **Enactment Drift**  | 執行中實際行為超出 Role State      | 執行後 evidence 比對 |

2. **以維度區分**（保留 §5.8 的 Viewpoint / Responsibility / Authority / Scope / Work / Interaction / Evidence Drift）。

3. 兩者形成 **locus × dimension 矩陣**，取代目前兩份重疊清單。跨模型、跨流程、跨執行等只是漂移的**觸發情境**，不是漂移類型。

4. **Role Fidelity** 目前定義為「degree」但無測度。若本文不打算給量測，改為「逐元素結構比對的通過／不通過」，避免引出量化期待。

### 2.4 Role Architecture 元組：分離設計時與執行時

`RA = (D, V, B, R, J, K, E)` 混合兩個層次。建議：

- **Design-time**：Role Definitions、版本譜系、角色間關係、契約與限制；
- **Run-time**：Bindings、Role States、Work Junctions、Evidence。

§3.4 的九種關係也應標明作用層次：`separates-from`、`escalates-to` 是 Definition 層宣告；`continues-from`、`produces-for` 在 State 層實現。並可將九種關係分為三類：**flow**（produces-for、continues-from、delegates-to）、**governance**（reviews、challenges、authorizes、accepts、escalates-to）、**constraint**（separates-from）。

若希望與 Engineering Determinacy 論文的「不使用公式」立場一致，可考慮將元組與 RoleValid 等式降為表格；若保留，至少讓符號在全文被實際使用（目前 RA 元組定義後未再引用）。

### 2.5 五項 Validity 條件的重新定位

保留，但改寫為**Role State 相對於 Role Definition 的 fidelity 檢查**，並對應到 binding 階段：

| 條件           | 檢查問題（改寫後）                                         | 主要時點                                 |
| -------------- | ---------------------------------------------------------- | ---------------------------------------- |
| Identity       | Role State 能否解析回唯一 Dᵥ？                             | 綁定前                                   |
| Responsibility | 實際承擔的責任是否等於 Definition 宣告？有無未承接的縮減？ | 綁定前／後                               |
| Authority      | 實際規則集與決策範圍是否 ⊆ Definition？                    | 綁定前／執行中                           |
| Capacity       | Actor 實際能力是否滿足 Required Capabilities？             | 綁定時（Actor 屬性，非 Definition 屬性） |
| Continuity     | 輸出是否連到 Definition 宣告的接收角色？                   | 執行後                                   |

如此一來，§4 成為漂移檢測的一部分，而非另起一套 accountability 理論。

---

## 3. Failure Modes 重新組織

§5 九項混合了靜態設計缺陷、綁定缺陷與漂移，且 Role Drift 僅為其中一項，削弱主軸。建議依 locus 重組：

| 類別                                | 項目                                                                                 | 備註                            |
| ----------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------- |
| **Definition 缺陷**（架構靜態錯誤） | Responsibility Vacancy（→DR-V）、Role Collision、Authority–Responsibility Divergence | SoD 部分須承認 RBAC 前作        |
| **Binding 缺陷**                    | Role Label Substitution、Persona–Standing Confusion、Capability-Blind Assignment     | 共同成因：以標籤取代 Definition |
| **Enactment 漂移**                  | 七種維度漂移、Orphaned Output                                                        | 本文主貢獻區                    |
| **衍生後果**                        | Accountability Laundering                                                            | 是上述缺陷的後果，非獨立類別    |

---

## 4. 例子（§6）調整

現例展示的是**單次流程的 validity 失敗**，沒有展示**跨情境漂移**，與標題不符。建議增加或改為：

- 同一 **Verification Role v1.2** 綁定到模型 A（repo X）與模型 B（repo Y）；
- 模型 B 在多次執行後開始輸出「建議可上線」，實質進入 Release Authorization 的決策範圍（Enactment / Authority Drift）；
- 由於兩個 Role State 皆可解析回 v1.2，比對 Evidence Record 即可偵測 B 的輸出型別超出 Output Contract、決策效果超出 Decision Right；
- 對照組：若角色僅以 prompt「You are a reviewer」存在，此漂移無比較基準，不可偵測。

原 caching 例子可保留為次要例子，並標註為 DR-O。

---

## 5. 建議章節架構

```
1. Introduction
   - 問題：角色標籤持續，角色意義被重新推論
   - 定位聲明：貢獻在 LLM 條件下的持久化與漂移控制，非角色結構本身
2. Why Role Meaning Drifts
   - 既有表示各只持久化一個維度
   - 機率性重建作為新條件
   - 與 Gaia / MOISE+ / RBAC / agent spec 的差異
3. Role Definition
   - Actor / Role Definition / Role State 三分
   - 四層元素模型與 minimum completeness
   - Authority / Decision Right / Scope 與 BRA、Behavior Space 的對應
4. Binding and Versioning
   - Bind 運算與單調性 invariant
   - Responsibility 不可單向縮減
   - 演化（versioned）vs 漂移（implicit）
5. Role Drift
   - locus × dimension 矩陣
   - Fidelity 檢查：五項條件改寫
6. Role Relations and Composition
   - flow / governance / constraint 三類；design-time vs run-time
7. Failure Modes（依 locus 重組）
8. Illustrative Application（以跨模型漂移為主例）
9. Evidence and Conformance（Evidence Record 對應三個 locus 的檢測時點）
10. Relationship to Prior Work in This Program
   - Engineering Determinacy 為上位原則；DA/DR、BRA、Scope、Anchor、Continuation Readiness 的對應
11. Propositions
12. Limitations
13. Conclusion
```

主要變動：§7（研究體系關係）往後移並精簡；Drift 從 §3.6 子節升為獨立章；五項條件併入 Drift 章。

---

## 6. Propositions 精簡

九項中，P1–P5 屬 B 線，P6–P9 屬 A 線。建議保留 5–6 項，以 A 線為主：

- **保留並強化**：P6（漂移只能透過版本化狀態偵測）、P8（跨模型重用需結構身分）、P9（顯式調整區分演化與漂移）
- **新增**：Responsibility 縮減須有承接（§2.2 invariant）
- **合併**：P1 + P4 → 「以標籤或 actor 類型取代 Role Definition 無法保證 fidelity」
- **移除或降級**：P2（permission ≠ authority 已是共識）、P5（SoD 結構性已見於 RBAC）

---

## 7. 其他

- **標題**：副標「Responsibility and Authority Drift」窄於正文的七種漂移維度。可考慮：*Role Architecture: Persistent Role Definitions Against Role Drift Across AI Models and Workflows*。
- **Abstract**：目前列舉 12 個元素與 5 項條件，過長。建議只保留：問題（標籤持久、意義漂移）→ 主張（Role Definition 作為持久工程物件）→ 機制（binding、versioning、fidelity 檢查）→ 定位（ED 的應用）。
- **Role Evidence Record**：12 個欄位可依三個 locus 標註用途，否則只是清單。
- **Capability**：明確放在 Actor／Role State，Definition 只承載 Required Capabilities，避免與 Definition 持久性混淆。

---

---

# v0.4 — 修訂筆記（2026-10-25）

> 對象：`2026-10_role-architecture.md`（概念稿）
> 範圍：只處理核心論點、概念模型與章節架構；不含文字潤飾、引用格式與文獻補齊細節。

---

## 0. 總評

稿件有兩條論點同時在跑，且彼此爭奪主軸：

| 論點線                                                                   | 出現位置                                | 問題                                                                       |
| ------------------------------------------------------------------------ | --------------------------------------- | -------------------------------------------------------------------------- |
| **A. Role Drift**：角色意義跨模型／流程重用時被重新推論而漂移            | 標題、Abstract、§3.6、§5.8、P8–P9、結論 | 是本文真正的新貢獻，但在正文中只占一節加一個 failure mode                  |
| **B. Role Validity**：一次行動是否由負責、有權、有能力、可延續的角色執行 | §2、§4、§5 大部分、§6 例子              | 與 Continuation Readiness、DA/DR 高度重疊，且 B 本身不需要「持久化」也成立 |

**建議：以 A 為唯一主軸，B 降為 A 的檢測手段。** 五項 validity 條件改寫為「Role State 是否忠於 Role Definition 的檢查維度」，而非獨立的 accountability 理論。否則審稿者會判定本文是 Continuation Readiness 的延伸，而非獨立貢獻。

主軸一句話建議改為（直接套用 Engineering Determinacy 的 model-independent determinacy）：

> **已確立的角色意義，不應因消費它的模型、流程或執行次數改變而改變。**

---

## 1. 核心論點調整

### 1.1 問題定義：從「表示不足」改為「重新推論」

§2 目前論證「職稱／權限／流程 lane／persona 不足以建立 accountability」，這是 B 線的論證。A 線應該論證的是：

- 每一種既有表示**只持久化角色的一個維度**（職稱→身分、RBAC→permission、lane→活動、persona→行為傾向、RACI→責任類別）；
- 其餘維度在每次使用時**由模型或人重新推論**；
- 重新推論在確定性執行者（傳統軟體、受訓人員）下相對穩定，在 LLM 下是機率性的 → 同一標籤產生不同 Role State。

這樣 §2 就直接導出 Role Drift，而不是導出「accountability 缺口」。

### 1.2 新穎性定位：必須正面處理 MAS 組織模型

目前 §11 只泛稱「需比對 role theory、RBAC、MAS…」。實際上有幾個前作與本文的 Role Definition 結構**非常接近**，審稿時必然被點名：

| 前作                                                       | 已具備                                                         | 本文需主張的差異                                                    |
| ---------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------- |
| Gaia（Wooldridge et al., 2000）                            | Role = responsibilities + permissions + activities + protocols | Gaia 假設 agent 以確定性方式實作 role；未處理機率性重建與跨模型漂移 |
| MOISE+ / OperA                                             | 角色、mission、norm、組織結構                                  | 同上；且無版本／binding／override 治理                              |
| NIST RBAC（含 SSD/DSD）                                    | 角色階層、static/dynamic separation of duties                  | SoD 已是成熟機制，本文 §5.6 Role Collision 不能當成新貢獻           |
| Agent 規格（A2A AgentCard、CrewAI role/goal/backstory 等） | 可重用的 agent 角色描述                                        | 屬 persona/能力宣告，無 authority、責任、版本漂移治理               |

建議明確宣告：**貢獻不在角色結構本身，而在「LLM 條件下角色意義的持久化、綁定與漂移控制」**。§11 第一段已有此意，應提前到 §1 作為定位聲明。

另：避免使用 **Role Engineering** 作為關鍵字，此詞在 RBAC 領域已有固定意義（Coyne, 1996），會造成誤讀。

### 1.3 與既有研究體系的術語衝突

| 衝突點                         | 現稿用法                                                                 | 既有 canonical 用法                                                                | 建議                                                                                                                                                  |
| ------------------------------ | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Authority**                  | 「可決定、核准、變更、拒絕或引發什麼」— 接近 decision right / permission | BRA：Authority = Policy (MUST) + Constraint (MUST NOT)，**不是** authorization     | 必須擇一。若保留 BRA 定義，則 Role Definition 中的 Authority 與 Constraints 應合併為「bound rule set」，另立 **Decision Right** 承載「可決定什麼」    |
| **Scope**                      | 單一 Applicable Scope                                                    | Visible Scope ≠ Artifact Scope                                                     | Role Definition 至少拆為 Visible Scope（可讀／可取證）與 Artifact Scope（可修改）；Behavior Space = Artifact Scope × Authority 可直接作為角色行為邊界 |
| **Responsibility Vacancy**     | §5.5 自行命名                                                            | DR-V（Decision Vacancy：Never Authorized / Lost in Transition / Implicit Handoff） | 直接引用 DR-V，並說明 Role Architecture 提供 DR-V 的角色層成因                                                                                        |
| **Authority Drift / 越權決策** | §5.8、§6.3 caching 例子                                                  | DR-O（Over Decision）                                                              | §6.3 的 Implementation Agent 選 caching strategy 是典型 DR-O，應明確對應                                                                              |
| **Role State**                 | 本文定義                                                                 | Continuation Readiness 已定義                                                      | 需說明本文定義是否擴充／修訂原定義，並保持欄位一致                                                                                                    |

---

## 2. 概念模型調整

### 2.1 Role Definition 元素分層

13 個元素平鋪，未區分核心與延伸，也無法支撐「minimum completeness」。建議分四層：

| 層                             | 元素                                                                                       | 性質                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **L1 Identity**                | Identity、Version、Description                                                             | 可解析性；漂移比較的錨點（對應 Anchor Architecture） |
| **L2 Semantic Core**           | Viewpoints、Work Definition、Responsibilities                                              | 最容易被機率性重建的部分；**漂移主要發生層**         |
| **L3 Governance Boundary**     | Authority（BRA rule set）、Decision Right、Visible / Artifact Scope、Required Capabilities | 綁定時的單調性檢查對象                               |
| **L4 Interface & Interaction** | Input/Output Contract、Interaction Rules、Escalation、Evidence Requirements                | 角色間組合與驗證                                     |

Minimum completeness = L1 + L2 + L3 必要；L4 依流程而定。

### 2.2 Binding 規則：補上單調性，並指出 Responsibility 的反例

`R = Bind(Dᵥ, A, C, O)` 目前只說 override 可「narrow」不可「silently expand」。這對 Scope 與 Authority 成立，**對 Responsibility 不成立**：

- Scope、Decision Right、Artifact Scope：binding 只可縮小（⊆）；
- Constraint（MUST NOT）：binding 只可增加；
- **Responsibility：縮小即產生 vacancy**。縮小責任必須同時宣告承接角色，否則等同 DR-V。

這是本文可以提出的一個非顯然論點，建議寫成明確的 binding invariant，而非僅一句「may narrow」。

### 2.3 Role Drift 操作化

現稿「effective meaning diverges」不可觀測。建議：

1. **以 locus 區分漂移類型**（取代 §3.6 的「across models/workflows/stages…」清單）：

| Locus                | 定義                               | 檢測時點             |
| -------------------- | ---------------------------------- | -------------------- |
| **Definition Drift** | 同一 identifier 下內容改變而未升版 | 版本比對             |
| **Binding Drift**    | 實例化時未宣告的擴張、替換或省略   | 綁定前 conformance   |
| **Enactment Drift**  | 執行中實際行為超出 Role State      | 執行後 evidence 比對 |

2. **以維度區分**（保留 §5.8 的 Viewpoint / Responsibility / Authority / Scope / Work / Interaction / Evidence Drift）。

3. 兩者形成 **locus × dimension 矩陣**，取代目前兩份重疊清單。跨模型、跨流程、跨執行等只是漂移的**觸發情境**，不是漂移類型。

4. **Role Fidelity** 目前定義為「degree」但無測度。若本文不打算給量測，改為「逐元素結構比對的通過／不通過」，避免引出量化期待。

### 2.4 Role Architecture 元組：分離設計時與執行時

`RA = (D, V, B, R, J, K, E)` 混合兩個層次。建議：

- **Design-time**：Role Definitions、版本譜系、角色間關係、契約與限制；
- **Run-time**：Bindings、Role States、Work Junctions、Evidence。

§3.4 的九種關係也應標明作用層次：`separates-from`、`escalates-to` 是 Definition 層宣告；`continues-from`、`produces-for` 在 State 層實現。並可將九種關係分為三類：**flow**（produces-for、continues-from、delegates-to）、**governance**（reviews、challenges、authorizes、accepts、escalates-to）、**constraint**（separates-from）。

若希望與 Engineering Determinacy 論文的「不使用公式」立場一致，可考慮將元組與 RoleValid 等式降為表格；若保留，至少讓符號在全文被實際使用（目前 RA 元組定義後未再引用）。

### 2.5 五項 Validity 條件的重新定位

保留，但改寫為**Role State 相對於 Role Definition 的 fidelity 檢查**，並對應到 binding 階段：

| 條件           | 檢查問題（改寫後）                                         | 主要時點                                 |
| -------------- | ---------------------------------------------------------- | ---------------------------------------- |
| Identity       | Role State 能否解析回唯一 Dᵥ？                             | 綁定前                                   |
| Responsibility | 實際承擔的責任是否等於 Definition 宣告？有無未承接的縮減？ | 綁定前／後                               |
| Authority      | 實際規則集與決策範圍是否 ⊆ Definition？                    | 綁定前／執行中                           |
| Capacity       | Actor 實際能力是否滿足 Required Capabilities？             | 綁定時（Actor 屬性，非 Definition 屬性） |
| Continuity     | 輸出是否連到 Definition 宣告的接收角色？                   | 執行後                                   |

如此一來，§4 成為漂移檢測的一部分，而非另起一套 accountability 理論。

---

## 3. Failure Modes 重新組織

§5 九項混合了靜態設計缺陷、綁定缺陷與漂移，且 Role Drift 僅為其中一項，削弱主軸。建議依 locus 重組：

| 類別                                | 項目                                                                                 | 備註                            |
| ----------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------- |
| **Definition 缺陷**（架構靜態錯誤） | Responsibility Vacancy（→DR-V）、Role Collision、Authority–Responsibility Divergence | SoD 部分須承認 RBAC 前作        |
| **Binding 缺陷**                    | Role Label Substitution、Persona–Standing Confusion、Capability-Blind Assignment     | 共同成因：以標籤取代 Definition |
| **Enactment 漂移**                  | 七種維度漂移、Orphaned Output                                                        | 本文主貢獻區                    |
| **衍生後果**                        | Accountability Laundering                                                            | 是上述缺陷的後果，非獨立類別    |

---

## 4. 例子（§6）調整

現例展示的是**單次流程的 validity 失敗**，沒有展示**跨情境漂移**，與標題不符。建議增加或改為：

- 同一 **Verification Role v1.2** 綁定到模型 A（repo X）與模型 B（repo Y）；
- 模型 B 在多次執行後開始輸出「建議可上線」，實質進入 Release Authorization 的決策範圍（Enactment / Authority Drift）；
- 由於兩個 Role State 皆可解析回 v1.2，比對 Evidence Record 即可偵測 B 的輸出型別超出 Output Contract、決策效果超出 Decision Right；
- 對照組：若角色僅以 prompt「You are a reviewer」存在，此漂移無比較基準，不可偵測。

原 caching 例子可保留為次要例子，並標註為 DR-O。

---

## 5. 建議章節架構

```
1. Introduction
   - 問題：角色標籤持續，角色意義被重新推論
   - 定位聲明：貢獻在 LLM 條件下的持久化與漂移控制，非角色結構本身
2. Why Role Meaning Drifts
   - 既有表示各只持久化一個維度
   - 機率性重建作為新條件
   - 與 Gaia / MOISE+ / RBAC / agent spec 的差異
3. Role Definition
   - Actor / Role Definition / Role State 三分
   - 四層元素模型與 minimum completeness
   - Authority / Decision Right / Scope 與 BRA、Behavior Space 的對應
4. Binding and Versioning
   - Bind 運算與單調性 invariant
   - Responsibility 不可單向縮減
   - 演化（versioned）vs 漂移（implicit）
5. Role Drift
   - locus × dimension 矩陣
   - Fidelity 檢查：五項條件改寫
6. Role Relations and Composition
   - flow / governance / constraint 三類；design-time vs run-time
7. Failure Modes（依 locus 重組）
8. Illustrative Application（以跨模型漂移為主例）
9. Evidence and Conformance（Evidence Record 對應三個 locus 的檢測時點）
10. Relationship to Prior Work in This Program
   - Engineering Determinacy 為上位原則；DA/DR、BRA、Scope、Anchor、Continuation Readiness 的對應
11. Propositions
12. Limitations
13. Conclusion
```

主要變動：§7（研究體系關係）往後移並精簡；Drift 從 §3.6 子節升為獨立章；五項條件併入 Drift 章。

---

## 6. Propositions 精簡

九項中，P1–P5 屬 B 線，P6–P9 屬 A 線。建議保留 5–6 項，以 A 線為主：

- **保留並強化**：P6（漂移只能透過版本化狀態偵測）、P8（跨模型重用需結構身分）、P9（顯式調整區分演化與漂移）
- **新增**：Responsibility 縮減須有承接（§2.2 invariant）
- **合併**：P1 + P4 → 「以標籤或 actor 類型取代 Role Definition 無法保證 fidelity」
- **移除或降級**：P2（permission ≠ authority 已是共識）、P5（SoD 結構性已見於 RBAC）

---

## 7. 其他

- **標題**：副標「Responsibility and Authority Drift」窄於正文的七種漂移維度。可考慮：*Role Architecture: Persistent Role Definitions Against Role Drift Across AI Models and Workflows*。
- **Abstract**：目前列舉 12 個元素與 5 項條件，過長。建議只保留：問題（標籤持久、意義漂移）→ 主張（Role Definition 作為持久工程物件）→ 機制（binding、versioning、fidelity 檢查）→ 定位（ED 的應用）。
- **Role Evidence Record**：12 個欄位可依三個 locus 標註用途，否則只是清單。
- **Capability**：明確放在 Actor／Role State，Definition 只承載 Required Capabilities，避免與 Definition 持久性混淆。

---

# v0.5 — Initial Review Draft（Superseded）

> **Status:** Superseded after the Role Inference Boundary and Stable Core + Extension Sections baselines were confirmed. Retained as review provenance; the active v0.5 review appears below.

| 項目     | 內容                                        |
| -------- | ------------------------------------------- |
| 版本     | **v0.5**                                    |
| 日期     | 2026-10-25                                  |
| 審核基準 | `2026-10_role-architecture_concept.md` v0.5 |
| 審核對象 | `2026-10_role-architecture.md`（概念稿）    |
| 欄位     | 位置、問題、原因、來源、調整方向            |

**來源代碼**
- `C§n`：Concept v0.5 第 n 節
- `BRA` / `VSS` / `BND`（Boundary as an Execution-Time Primitive） / `SCP`（Scope as a Governance Primitive） / `ED`（Engineering Determinacy） / `DR` / `CR`（Continuation Readiness） / `CFGA`：既有研究的 canonical 定義
- `EXT`：外部前作

---

## 總結

審核對象的重心在 **accountability / role validity**（§2、§4、§5、§6 占大部分篇幅），與 Concept v0.5 的兩個目的（boundary 工程化、可擴展可共享）不一致。其中，**可擴展與可共享在審核對象中幾乎不存在**。

| 優先級           | 項目數 | 說明                            |
| ---------------- | ------ | ------------------------------- |
| P0（主軸）       | 4      | 不調整則論文定位錯誤            |
| P1（模型）       | 8      | 概念模型缺漏或與 canonical 衝突 |
| P2（結構與呈現） | 8      | 章節、例子、命題、標題          |

---

## A. 主軸（P0）

| ID   | 位置                        | 問題                                                 | 原因                                                                             | 來源      | 調整方向                                                                                               |
| ---- | --------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| A-01 | 全文、Abstract、§1 研究問題 | 主軸是「保留 accountability、防止責任與權限漂移」    | 偏離核心命題；accountability 屬於 DA/DR 與 CR 的範圍，留在本文會被視為 CR 的延伸 | C§1、C§10 | 主軸改為「role 從標籤變成 boundary」與「role 可擴展、可共享」；accountability 降為 boundary 失效的後果 |
| A-02 | §1                          | 缺少「prompt 中是小事、agentic flow 中是大事」的論證 | 這是全文的動機起點；沒有它，role 工程化的必要性不成立                            | C§2       | 新增放大條件（修正迴路、輸出性質、錯誤傳遞、多 agent、重複、換模型），並以「你是一個 PM」作為開場例    |
| A-03 | 全文                        | 缺少可擴展機制（繼承、組合、override 規則）          | 目的二完全沒有實現；「reusable」只出現在定義中                                   | C§5       | 新增 Role Specialization、Role Composition、Role Substitution Rule 專章                                |
| A-04 | 全文                        | 缺少共享機制（Role Library）                         | 目的二的共享面沒有實現；也沒有說明與 BRA Rule Library 的關係                     | C§6、BRA  | 新增 Role Library 專章：分層、版本 pin、升版規則、跨組織在地化                                         |

---

## B. 概念模型（P1）

| ID   | 位置                           | 問題                                                                                  | 原因                                                                                         | 來源          | 調整方向                                                                                                                   |
| ---- | ------------------------------ | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------- |
| B-01 | §3.2 元素表                    | 13 個元素平鋪，沒有分層，也沒有核心與延伸之分                                         | 無法支撐最小完整性，也看不出 role 是什麼的 boundary                                          | C§3.1、C§11-4 | 收斂為 Identity/Version + Viewpoint / Behavior / Work 三種 Boundary                                                        |
| B-02 | §3.2、§3.3 Authority           | Authority 定義為「可決定、核准、變更什麼」                                            | 與 BRA canonical 衝突：Authority = Policy (MUST) + Constraint (MUST NOT)，不是 authorization | BRA           | 改採 BRA 定義；Constraints 併入 Behavior Boundary；「可決定什麼」若需要，另立名稱                                          |
| B-03 | §3.2 Applicable Scope          | 只有單一 Scope                                                                        | 與 canonical 衝突：Visible Scope ≠ Artifact Scope；也沒有用到 Behavior Space                 | SCP、C§3.2    | 拆成 Visible / Artifact Scope；Behavior Boundary 以 Behavior Space = Artifact Scope × Authority 表達                       |
| B-04 | §3.1、§3.2                     | Prompt 與 Role Definition 的關係只用一句「not a prompt template」帶過                 | 沒有建立「prompt 是實作、不是來源」，ED 的 model-independent determinacy 沒有被用上          | C§3.4、ED     | 新增一節：Role Definition 為 interface，prompt / agent config 為 implementation                                            |
| B-05 | §3.1                           | Actor / Role Definition / Role State 三分正確，但沒有用 class / instance 框架         | 錯過與目的二（OO）的銜接                                                                     | C§4           | 保留三分，改用 Class / Binding / Instance 說明                                                                             |
| B-06 | §3.3 Capability、§4.4          | Capability 同時出現在 Definition 與 Validity 條件中                                   | 混淆了 Definition 的持久性與 Actor 的實際狀態                                                | C§4           | Definition 只放 Required Capabilities；實際能力屬於 Actor / Role State，在 binding 時檢查                                  |
| B-07 | §3.6 Bind / override           | 只說 override「may narrow, must not silently expand」                                 | 沒有區分方向：Scope 可縮、Constraint 只增；責任縮小則會造成 vacancy                          | C§5.4、DR     | 寫成明確的 binding override 規則，並與 Substitution Rule 同向                                                              |
| B-08 | §3.6 Role Drift、Role Fidelity | 漂移以「effective meaning diverges」定義，不可觀測；Fidelity 用「degree」，但沒有測度 | 無法操作；會引出量化期待                                                                     | C§7、C§10     | Drift 依 Definition / Binding / Enactment 分類；以 Substitution Rule 作為演化與漂移的判準；Fidelity 改為逐元素比對，或刪除 |

---

## C. 章節與內容處置（P2）

| ID   | 位置                    | 問題                                                                       | 原因                                                     | 來源                         | 調整方向                                                                                                                                                                         |
| ---- | ----------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| C-01 | §2                      | 論證「職稱、RBAC、lane、persona、HITL 不足以建立 accountability」          | 屬於 A-01 的偏離；HITL 與本文目的無關                    | C§2、C§10                    | 改寫為「既有表示各只固定 role 的一個面向，其餘留給模型推論」；刪除 §2.5 HITL                                                                                                     |
| C-02 | §3.4 Role Relations     | 九種關係，沒有分類，也沒有區分設計時與執行時                               | 超出本文範圍，稀釋主軸                                   | C§10、C§11-5                 | 保留 escalates-to、produces-for、separates-from；其餘移入未來工作                                                                                                                |
| C-03 | §3.5 RA 元組            | 元組定義後全文沒有再使用；混合設計時與執行時                               | 形式化沒有發揮作用                                       | C§4、C§6                     | 改為 Role Library + Binding + Role State 的結構說明                                                                                                                              |
| C-04 | §4 五項 Validity 條件   | 獨立成為 accountability 檢驗理論                                           | 與 CR、DA/DR 重疊；不是本文目的                          | C§10、CR                     | 刪除，或縮成一節「binding 檢查」；交接有效性引用 CR                                                                                                                              |
| C-05 | §5 九項 Failure Modes   | 混合了 accountability 缺陷與 boundary 缺陷；Role Drift 只是其中一項        | 削弱主軸；部分與 DR、RBAC SoD 重疊                       | C§7、DR、EXT（RBAC SSD/DSD） | 只保留 Label Substitution、Persona–Standing Confusion、Role Drift；Responsibility Vacancy 改引用 DR-V；Accountability Laundering、Orphaned Output、Role Collision 刪除或改為引用 |
| C-06 | §6 software-change 例子 | 展示單次流程的 validity 失敗，沒有展示 boundary 定義、繼承與跨模型 binding | 與兩個目的都不對應                                       | C§3.3、C§5.3                 | 改為：PM 標籤 vs PM@1.0 對照 → Technical-PM 繼承 → 同一 role 綁定兩個模型；caching 例可刪，或作為 DR-O 的附註                                                                    |
| C-07 | §7 研究體系關係         | 缺少 Boundary 論文與 CFGA；ED 放在最後一小節                               | Boundary absence 是本文問題定義的直接來源；ED 是上位原則 | C§8、BND、ED、CFGA           | ED 提到上位；新增 BND（boundary absence）、CFGA（組合衝突）；CR 的關係改寫為「Role State 由 Role Definition 實例化」                                                             |
| C-08 | §9 Role Evidence Record | 12 個欄位，偏 accountability 稽核                                          | 與本文目的不符                                           | C§4、C§7                     | 精簡為 binding 紀錄：Role ID、version、override、model、flow、時間                                                                                                               |

---

## D. 命題、定位、標題（P2）

| ID   | 位置                 | 問題                                                                                   | 原因                                                                                | 來源               | 調整方向                                                                                                                  |
| ---- | -------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| D-01 | §10 P1–P9            | P1–P5 屬於 accountability 線；P2（permission ≠ authority）、P5（結構性 SoD）是既有共識 | 命題與主軸不一致；新穎性不足                                                        | C§1、C§5、C§6、EXT | 重寫為：boundary absence、prompt 為實作、Substitution Rule、Constraint 只增不減、Library 以引用組裝、共享 role 變更須升版 |
| D-02 | §1、§11 新穎性       | 定位放在 §11；沒有正面處理 Gaia、MOISE+、RBAC hierarchy、agent spec                    | 審稿時必然被點名；RBAC 也有繼承                                                     | C§9、EXT           | 定位聲明移到 §1；比較表聚焦在「boundary、繼承限制、library、跨模型 binding」的差異                                        |
| D-03 | 標題、副標           | 副標「Prevent Responsibility and Authority Drift」                                     | Drift 是症狀不是目的；也窄於三種 boundary                                           | C§1、C§7           | 建議：*Role Architecture: Engineering Bounded, Extensible, and Shareable Roles for AI Agents and Agentic Workflows*       |
| D-04 | Abstract             | 列舉 12 個元素與 5 項條件；以 accountability 收尾                                      | 過長；主軸錯誤                                                                      | C§1                | 結構：prompt role 是標籤 → agentic 放大 → Role 作為 boundary → 繼承、組合、Library → ED 的應用                            |
| D-05 | Keywords             | 含 Role Engineering、Responsibility、Authority 等                                      | Role Engineering 是 RBAC 既有用語（Coyne, 1996），會造成誤讀；其餘偏 accountability | EXT、C§1           | 移除上述詞；加入 Role Library、Role Specialization、Boundary、Agentic Workflow、Prompt Role                               |
| D-06 | §8 Design Principles | 八項原則偏 accountability，沒有涵蓋擴展與共享                                          | 與兩個目的不一致                                                                    | C§3–C§6            | 改寫為 boundary、繼承、組合、版本、共享相關原則，或併入命題                                                               |
| D-07 | §11 Limitations      | 研究議程以 accountability 驗證為主                                                     | 與主軸不一致                                                                        | C§10、C§11         | 改用 Concept 的開放問題：OO 比喻限度、多重繼承、參數化 Scope、最小完整性                                                  |
| D-08 | §12 Conclusion       | 收尾問題聚焦 fidelity 與 accountability                                                | 與核心命題不一致                                                                    | C§1                | 以核心命題收尾：role 從標籤變成 boundary，並可像 class 與 rule 一樣擴展與共享                                             |

---

## E. 保留項目

以下內容與 Concept v0.5 一致，建議保留，只做銜接調整：

| 位置       | 內容                                                | 備註                                    |
| ---------- | --------------------------------------------------- | --------------------------------------- |
| §3.1       | Actor / Role Definition / Role State 三分           | 改用 class / instance 說明（B-05）      |
| §3.2 後段  | Viewpoint 必須逐一列出；Work 與 Responsibility 分離 | 併入三種 Boundary                       |
| §3.6 前段  | Persistence 不等於 immutability；變更必須明確       | 與升版規則合併                          |
| §5.1、§5.4 | Role Label Substitution、Persona–Standing Confusion | 作為 boundary absence 的具體表現        |
| §5.8       | 七種 drift 維度                                     | 收斂為 Viewpoint / Behavior / Work 三類 |
| §6.2 末段  | 同一 Verification Role 綁定不同模型                 | 可作為新例子的基礎                      |

---

## F. v0.5 內容檢核問題

- [ ] **審核基準版本不符。** v0.5 review 的多數位置與問題描述對應較早期 manuscript，而非目前已完成 v0.4 的 `2026-10_role-architecture.md`；待確認是否應以目前 manuscript 重新產生差異清單。

- [ ] **A-01 對目前主軸的判讀已不成立。** 現稿已以 Role Drift 與 persistent Role Definition 為主，accountability 已降為衍生問題；待確認要改成「v0.5 Concept 有意改變 v0.4 thesis」，而不是描述為現稿仍以 accountability 為主。

- [ ] **B-01、B-02、B-03、B-04、B-06 與現稿內容不符。** 現稿已有四層 Definition、BRA Authority、Decision Right、Visible／Artifact Scope、prompt-as-binding-artifact 與 Required Capability／Actor capability 分離；待逐項刪除已完成項目，只保留 Concept v0.5 真正新增的三 Boundary 收斂要求。

- [ ] **B-08 已被 v0.3／v0.4 解決。** 現稿已有 Definition／Binding／Enactment loci、dimension matrix 與 categorical Fidelity；待確認 review 不應再稱其為不可觀測或未量測的 degree。

- [ ] **C-02、C-03、C-04 的章節位置與狀態過期。** 現稿的 Role Relations 已在 §6 分類並區分 design/run time，RA tuple 已移除，五項 validity 已降為 §5.4 fidelity checks；待改成 v0.5 Concept 要求的「再縮減或移出」而不是「尚未分類／仍是獨立理論」。

- [ ] **C-06 對案例的描述過期。** 現稿 §8 已是 Verification Role v1.2 跨 Model A／B 的 drift 案例，不再是單次 software-change validity 案例；待確認 review 應要求把案例改成 PM／Technical-PM specialization，或在既有跨模型案例上增加 inheritance，而非宣稱跨模型案例不存在。

- [ ] **D-01、D-03、D-04、D-05 的現況描述過期。** 現稿已有六項 drift-focused propositions、新的 Role Drift title、精簡 Abstract，且 Keywords 已移除 Role Engineering；待依 Concept v0.5 的新 thesis 說明「為何還要再改」，不要以已不存在的內容作為理由。

- [ ] **Review 將 Concept 的主張直接視為 canonical，缺少 concept-validity gate。** 即使暫不考量 issue 文件，review 仍應區分「Concept v0.5 新增要求」與「既有研究 canonical 衝突」；待確認 A–D 表中的來源欄不能僅用 `C§n` 就把新主張當成已確立規則。

- [ ] **P0／P1／P2 統計雖與表格列數相符，但沒有區分 resolved、regression 與 thesis change。** 待確認新增狀態欄，標示每項是 v0.4 已解決、v0.5 要求撤回、或 v0.5 新增，否則無法作為實際修訂清單。

---

# v0.5 — Revised Review（2026-10-25）

| 項目 | 內容 |
| --- | --- |
| 版本 | **v0.5** |
| 審核基準 | `2026-10_role-architecture_concept.md` v0.5 revised baseline |
| 審核對象 | `2026-10_role-architecture.md` v0.4 conceptual manuscript |
| Issue 處理 | 本節依使用者要求，不以 `2026-10_role-architecture_issue.md` 的未決研究問題否決 Concept |
| 審核性質 | 只列 Concept v0.5 與 manuscript v0.4 的有效差異 |

---

## 總結

目前 manuscript v0.4 已完成 persistent Role Definition、Definition／Binding／Enactment Drift、Decision Right、Visible／Artifact Scope、cross-model case 與 categorical Fidelity，因此不需要回退到早期 review 所描述的缺陷修補。

Concept v0.5 是一次新的 thesis refocusing：

> **從「以 persistent Role Definition 偵測 Role Drift」轉向「以 Role Inference Boundary 固定 Role meaning，並以 Stable Core、Extension Sections、specialization、composition 與 Role Library 支援擴充及共享」。**

Role Drift 仍保留，但由 architecture purpose 改為主要 failure condition。v0.5 manuscript 的工作不是重做 v0.3／v0.4，而是保留既有成果並改變其組織中心。

| 優先級 | 項目數 | 說明 |
| --- | --- | --- |
| P0 — Thesis | 4 | 不處理會使 v0.5 manuscript 與 Concept 主軸不一致 |
| P1 — Architecture | 7 | Stable Core、Extension、specialization、composition、library 的必要模型 |
| P2 — Structure | 6 | 章節、案例、命題、標題與研究關係調整 |

---

## A. Thesis Refocusing（P0）

| ID | Manuscript 現況 | Concept v0.5 要求 | 調整方向 |
| --- | --- | --- | --- |
| A-01 | Title、Abstract、§1、§5 與 Conclusion 以 Role Drift 為 primary architecture problem | Architecture purpose 是 Role Inference Boundary 工程化及 Role 的可擴展／可共享；Drift 是 failure condition | 改寫 title、research question、contributions 與 conclusion；保留 drift model 作為驗證 architecture 必要性的分析工具 |
| A-02 | Role Definition 被描述為 persistent comparison target | Role Definition 首先是限制 context-based role reconstruction 的 inference boundary | 新增 Role Inference Boundary 定義，明確區分 Role meaning inference 與 Task Execution Boundary |
| A-03 | 問題開場是 Verification Role 的跨模型 release recommendation drift | 動機應先展示 Role label 的意義全部來自 context，再說明 agentic flow 如何放大 variation | 以 `PM`／`Reviewer` label 為起點，加入 context sources 與 Implicit Decision-Right Expansion causal chain；cross-model validator case 可保留為後段 drift evidence |
| A-04 | Reuse 主要是 versioned binding | Reuse 還包括 specialization、composition、schema-governed extension 與 Role Library | 將 extensibility／shareability 升為 contribution，不只當 future work |

---

## B. Architecture Model（P1）

| ID | Manuscript 現況 | Concept v0.5 要求 | 調整方向 |
| --- | --- | --- | --- |
| B-01 | §3 使用 L1 Identity／L2 Semantic Core／L3 Governance Boundary／L4 Interface 四層 | `Role Definition = Stable Core + Extension Declarations + Referenced Extensions` | 以新模型取代四層作為 primary representation；可在討論中說明四層元素如何遷移到 Core 或 Extension |
| B-02 | Scope、Work、Evidence、Interaction 為 Definition 的固定 elements | Scope、Work 等屬 schema-governed Extension Sections，可事後擴充 | 新增 extension identity、schema、version、source、compatibility 與 unresolved semantics |
| B-03 | §3.5 直接把 Artifact Scope 與 Authority 組成 preliminary Behavior Space | Role Inference Boundary 不等同 Task Execution Boundary；Behavior Space 不是本 Concept 的必要 canonical 公式 | 移除或降為 future formalization；Scope Extension 只提供 Role-level declaration，runtime boundary 由既有 Boundary Architecture 解析 |
| B-04 | Prompt、tool policy、workflow node 已被視為 binding artifacts | Concept 要求更強的 interface／implementation 區分 | 保留並前移：Role Definition／Binding 是 source，prompt／agent config／tool policy 是 model-specific implementation artifacts |
| B-05 | Binding invariants 已明確，但 Definition 被視為封閉元素集合 | Override 必須同時符合 Stable Core 不可漂移與 Extension Schema 的允許方向 | 重寫 binding table：Core change → new version；Extension value → schema／parameter binding；undeclared completion → Binding Drift |
| B-06 | Role State canonical fields 已保留 | Concept 新增 extension／binding metadata 但不改寫 CR | 保留現稿 §3.1 的 canonical alignment；加入 extensions、dependency versions 與 generated implementation artifacts references |
| B-07 | Evidence 以 Definition／Binding／Enactment drift detection 為中心 | 仍需 evidence，但最小 binding record 應支持 Role Inference Boundary reconstruction | 保留三類 evidence，補上 Role ID、version、extension locks、model、flow、time、override；避免擴張成新的 accountability theory |

---

## C. Extensibility and Sharing（P1）

| ID | 缺少內容 | Concept v0.5 要求 | 調整方向 |
| --- | --- | --- | --- |
| C-01 | 沒有 Role Specialization model | child Role 必須通過逐元素 substitution compatibility | 新增 specialization 專章；處理 Required Viewpoints、Policy／Constraint、Responsibility、Decision Right、Scope 與 contract variance |
| C-02 | Responsibility transfer 目前只存在 binding invariant | Responsibility transfer 不等於 child 可替代 parent | 把 transfer 放在 composition／binding；specialization 必須保留 parent Responsibility |
| C-03 | 沒有 Role Extension object | Scope／Work／Evidence／Interaction／Capability 可由 schema 擴充 | 定義 Extension Declaration、Extension Instance、dependency lock 與 compatibility result |
| C-04 | Role composition 僅以 relations 表示 | Role 由 Core、Extensions 與 referenced Application Ruleset 組合 | 新增 composition model；直接規則矛盾判為 unsatisfiable，不以 MUST NOT 自動覆蓋 MUST |
| C-05 | 沒有 Role Library | 共享需 identifier、version、dependencies、pinning 與 migration | 新增 Role Library 專章，並與 BRA Rule Library／Application Ruleset 分工 |
| C-06 | 跨組織 reuse 僅在 Limitations 提及 | 可共享完整 Definition、parameterized template 或 abstract Role | 新增 locality／parameterization；在地化涵蓋 Scope、Authority、Decision Right、Responsibility、Evidence、ontology、legal context |

---

## D. Existing Content Disposition（P2）

| ID | 現有內容 | 處置 |
| --- | --- | --- |
| D-01 | §2 partial representations and repeated inference | 保留；加入 context sources 與 agentic risk amplification，並刪除「LLM 是唯一會 drift 的 actor」暗示 |
| D-02 | §4 Binding and Versioning | 保留並重寫為 Core／Extension binding；保留四種 binding outcomes 與 explicit Responsibility acceptance |
| D-03 | §5 locus × dimension drift model | 保留但降為 failure analysis；evolution、substitution compatibility、drift 必須分開判定 |
| D-04 | §5.4 Five Fidelity Checks | 縮短為 binding／enactment conformance checks；不得重新擴張為 accountability theory |
| D-05 | §6 Role Relations | 移至 extension／future work；正文只保留 `produces-for`、`escalates-to`、`separates-from` 等支持 composition 的最小關係 |
| D-06 | §7 Failure Modes | 大幅精簡；保留 Role Label Substitution、Persona–Standing Confusion、Role Drift，DR-V／DR-O 只作既有後果引用 |
| D-07 | §8 Verification Role case | 保留跨模型 drift 部分，前置加入 PM label → PM Definition → Technical-PM specialization → model bindings 的完整案例 |
| D-08 | §9 Evidence and Conformance | 保留可檢查性，但聚焦 inference boundary、binding 與 extension identity，不宣稱觀察 internal reasoning |

---

## E. Title、Propositions and Positioning（P2）

### Suggested title

> **Role Architecture: Engineering Bounded, Extensible, and Shareable Roles for AI Agents and Agentic Workflows**

### Suggested contribution sequence

1. Context-based Role inference and Role Inference Boundary.
2. Stable Core plus schema-governed Extension Sections.
3. Role Specialization and Substitution Compatibility.
4. Role Composition and BRA Application Ruleset integration.
5. Role Library, version pinning, parameterization, and sharing.
6. Role Drift as the failure condition exposed by absent or violated inference boundaries.

### Suggested propositions

- **P1 — Label insufficiency:** A Role label cannot preserve Role meaning when interpretation is reconstructed from context.
- **P2 — Inference-boundary determinacy:** An engineered Role constrains Role inference independently of the consuming model.
- **P3 — Explicit extension:** Scope、Work 與其他 domain structures may expand only through declared Extension Schemas, not contextual completion.
- **P4 — Substitution compatibility:** A specialized Role can replace its parent only when parent responsibilities, constraints, Decision Rights, and interfaces remain compatible.
- **P5 — Composition separation:** Role composition references BRA Application Rulesets and does not create a second atomic-rule composition authority.
- **P6 — Shareable identity:** A shared Role remains the same Role only when Definition and dependency identities are pinned or migrated explicitly.
- **P7 — Drift distinction:** Unversioned or unattributed Role meaning change is drift; a versioned breaking change may be governed evolution even when it is not substitutable.

### Prior-work positioning

保留現稿已建立的 Gaia、MOISE+、OperA、RBAC、role engineering、A2A 與 CrewAI 比較，但調整差異主張：

- 不宣稱 MAS Agent 必然 deterministic；
- 不把 AgentCard 簡化為純 persona；
- 不忽略 RBAC constraints、hierarchy、SSD／DSD；
- 新穎性聚焦 Role Inference Boundary、Extension Schema、cross-model binding 與 Role Library semantics。

---

## F. Open Questions, Not Immediate Defects

以下屬 Concept 已明列的 future research，不能在 v0.5 manuscript 中假裝已解決：

- Role Inference Boundary 的可觀測 conformance proxy；
- semantic／bindable／executable completeness 分層；
- multi-parent specialization conflict；
- parameterized Scope authorization；
- extension version propagation；
- minimal Role relation set。

本次重新檢核未發現 Concept v0.5 內部需要額外追加的 blocking issue；未決事項已記錄於 issue 文件與 Concept open questions。
