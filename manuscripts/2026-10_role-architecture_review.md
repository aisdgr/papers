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

---

# v0.5 — 定位重新聚焦（2026-10-25）

> 本節記錄對論文核心動機與目的的重新表述，作為後續改稿的定向依據。

---

## 0. 核心問題的重新表述

當我在 prompt 中寫下：

> 「你是一個 PM，請幫我……」

PM 的**觀點、權責、行為範圍**都會因模型版本、上下文、任務描述的措辭而有不同解讀。在單次 prompt 互動中，這種不確定性是可接受的小問題——人類在下一輪可以立刻修正。

**但在 agent 與 agentic flow 中，這成為大問題：**

- 同一個「PM Agent」被多個流程節點呼叫，各節點對其決策邊界的假設不一；
- 跨模型重用時，同一標籤在不同模型下推論出不同的責任與權限範圍；
- 流程自動化後無人在場即時修正，漂移累積而不可偵測；
- 事後追責時無法判斷某決策是否在該角色的授權範圍內。

**這是本文的真正問題陳述：prompt 中的角色描述，不足以作為 agentic flow 的工程邊界。**

---

## 1. 三個目的（重新定位）

### 目的一：Role Boundary 工程化

給角色一個可明確宣告、可比對、可驗證的邊界，使得：

- 一個角色「應該做什麼／不應該做什麼／有權決定什麼」是在執行前已定義的工程物件，而非每次由模型重新推論；
- 邊界的守護不依賴模型的善意解讀，而是結構上可稽核的（Evidence Record、Output Contract、Decision Right）；
- 對應 v0.4 §2.3 的 Enactment Drift 偵測機制。

**與 prompt engineering 的區別：** prompt 是給模型的指令；Role Definition 是給**流程設計者與審計者**的工程規格，兩者層次不同。

### 目的二：可擴展（Extensibility）

Role Definition 的設計參考 BRA 中 rule 的結構——rule 本身是原子可組合的，多條 rule 疊加形成角色的行為空間。類比至物件導向：

- Role Definition ≈ 類別（class）定義，宣告屬性與方法邊界；
- Binding ≈ 實例化（instantiation），將定義綁定至特定 actor／context；
- Override / Narrowing ≈ 繼承與覆寫，但有單調性約束（不可靜默擴展）；
- Role Composition（flow / governance / constraint 關係）≈ 物件間的關聯與委派。

這個設計使得角色可以逐層精化，而不必每次從零描述——複雜 agentic flow 中的角色體系因此具備工程可管理性。

### 目的三：可分享（Shareability）

類比 BRA 的 rule library：

- 一套「Verification Role」的定義，可以在不同產品、不同團隊的 agentic flow 中被引用，而不必各自重寫；
- 版本化（versioning）確保引用方知道自己用的是哪一個語意版本；
- 引用時的 binding 可做局部調窄（narrow），適應特定部署情境，同時保留對原 Definition 的可追溯性；
- 這使得 Role Definition 成為可在組織或社群中流通的**角色知識單元**，而非散落在各個 prompt 中的一次性描述。

---

## 2. 對 v0.4 建議的影響

| v0.4 建議                | v0.5 視角下的調整優先序                                                            |
| ------------------------ | ---------------------------------------------------------------------------------- |
| 以 Role Drift 為唯一主軸 | **維持**，但動機應從「prompt 不足」重寫為「agentic boundary 缺失」                 |
| Binding 單調性 invariant | **提升優先**：這是目的一（工程化邊界）的核心機制                                   |
| 四層元素模型（L1–L4）    | **維持**，強調 L3 Governance Boundary 是工程化邊界的承載層                         |
| 與 BRA rule 的對應       | **明確展開**：目的二（可擴展）需要在 §3 Role Definition 中正面呈現此類比           |
| Rule Library 類比        | **新增**：目的三（可分享）在 §4 Binding and Versioning 中補充 library / reuse 場景 |
| §1 定位聲明              | **重寫**：從「LLM 條件下的持久化」→「agentic flow 中的角色邊界工程化」             |

---

## 3. 建議的一句話主張（更新）

> **在 agentic flow 中，角色的邊界必須是顯式工程化的，而非由模型在執行時推論；Role Definition 是這個邊界的持久工程物件，支援精化、組合與跨流程重用。**
