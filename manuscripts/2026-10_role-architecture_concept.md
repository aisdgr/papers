# Role Architecture — Concept

## v0.5 — Role Inference Boundary and Extensible Role Structure

| 項目     | 內容                                                                           |
| -------- | ------------------------------------------------------------------------------ |
| 版本     | **v0.5**                                                                       |
| 日期     | 2026-10-25                                                                     |
| 性質     | 核心思維與概念架構定義；作為論文稿（`2026-10_role-architecture.md`）的審核基準 |
| 對應審核 | `2026-10_role-architecture_review.md` v0.5                                     |

---

### 1. 核心命題

> **A prompt role is a label whose meaning the model infers from context. An engineered Role establishes the boundary within which that role meaning may be inferred.**

Role Architecture 建立的是 **Role Inference Boundary**，不是 Task Execution Boundary。

- **Role Inference Boundary** 約束模型如何理解、補全與實例化一個 Role。
- **Task Execution Boundary** 約束 Actor 在特定任務執行時實際可以觀察、操作與影響什麼。

兩者的結構關係是：

> **Role Definition → Role Inference Boundary → Role State → Task Execution Boundary**

Role Definition 提供 Role 層級的語義、規則與可擴充結構；Binding 把它與 Actor、model、flow、task context 結合成 Role State；Role State 再與 task-specific Scope、constraints、runtime context 共同參與 Task Execution Boundary 的解析。

因此，Role 不直接等同 Execution Boundary，也不取代 Boundary Architecture。

Role Architecture 有兩個目的：

1. **Role Inference Boundary 工程化**：讓 Role 從由模型自由解讀的語意標籤，變成有持久推論邊界的工程物件。
2. **可擴展、可共享**：讓 Role 具有穩定核心，並透過明確、schema-governed 的 extension sections、specialization、composition 與 Role Library 重用。

---

### 2. 問題情境：Role 意義來自上下文

在 prompt 或 agentic flow 中，如果 Role 只有名稱而沒有獨立 Role Definition，模型只能從當前上下文重建 Role 的意義。

上下文可能包含：

- user task；
- system prompt；
- conversation history；
- retrieved context；
- available tools；
- workflow position；
- upstream Agent output；
- downstream output expectation；
- 以及模型自身對職稱與專業角色的既有理解。

因此，同一個 `PM`、`Reviewer` 或 `Architect` 標籤，在不同模型、不同 flow、不同 stage 或不同 execution 中，可能形成不同的 effective Role。

典型因果鏈為：

> **Abstract Role Label → Context-Based Role Inference → Different Effective Role Meaning → Role Drift → Implicit Decision-Right Expansion**

**Implicit Decision-Right Expansion** 是指模型從上下文推論出 Role 擁有原本未被明確授予的決定、核准、拒絕、接受或改變權。它不同於 technical permission expansion：工具權限可能完全沒有改變，但模型已把分析任務解讀為決策任務，或把 verification result 表述成 release recommendation。

#### 2.1 Agentic flow 的風險放大條件

單次 prompt 與 agentic flow 不是本質上互斥的兩種系統；下列是常見的風險放大條件，而不是絕對差異。

| 放大條件 | 較受控情境                          | 較高風險情境                               |
| -------- | ----------------------------------- | ------------------------------------------ |
| 修正迴路 | 每一步有人檢視並修正                | 多步自主執行，錯誤在人工介入前已傳遞       |
| 輸出效果 | 輸出只供人閱讀                      | 輸出觸發工具、修改 artifact 或成為下游前提 |
| 角色數量 | 單一 Actor／單次解讀                | 多 Agent 分別重建同一 Role label           |
| 重複使用 | 一次性使用                          | 同一 Role 在多次 execution 中反覆重建      |
| 模型替換 | Role meaning 由外部 Definition 固定 | Role meaning 隨 model interpretation 改變  |
| 流程位置 | 任務與權責由人即時說明              | workflow position 被模型用來推論未宣告權責 |

**結論：在缺少 Role Inference Boundary 時，context variation 會轉化為 Role meaning variation；在 agentic flow 中，這種 variation 更容易累積為可執行的 Decision-Right Expansion。**

只有 Role label，不代表整個 Task Execution Boundary 不存在。系統仍可能透過 task specification、BRA rules、tool permissions 或 runtime controller 建立 Execution Boundary。缺少的是 **Role Inference Boundary**：模型不知道該如何在那些 execution constraints 中理解自己扮演的 Role。

---

### 3. Role Definition：Stable Core + Extension Sections

Role Definition 不是封閉欄位清單，而是：

> **Role Definition = Stable Core + Extension Declarations + Referenced Extensions**

#### 3.1 Stable Core

Stable Core 保存不能在每次使用時重新推論的 Role meaning：

| 元素                       | 作用                                                                     |
| -------------------------- | ------------------------------------------------------------------------ |
| **Identity**               | 提供可解析的 Role identifier                                             |
| **Version**                | 區分已接受的 Role Definition state                                       |
| **Description**            | 說明 Role 的組織目的與語義定位                                           |
| **Required Viewpoints**    | 限制 Role 必須採取的 interpretive perspectives                           |
| **Responsibilities**       | 明定 Role 必須承擔的 outcomes、judgments 或 obligations                  |
| **Authority**              | 引用 BRA 的 Policy (MUST) 與 Constraint (MUST NOT) 結構                  |
| **Decision Rights**        | 明定 Role 可以決定、核准、拒絕、接受或觸發什麼                           |
| **Extension Declarations** | 宣告可附加的 extension type、schema、default state 與 compatibility rule |

Stable Core 建立 Role Inference Boundary。Context 可以在此邊界內具體化 Role，但不能自行增加 Required Viewpoint、Responsibility、Authority 或 Decision Right。

#### 3.2 Extension Sections

Scope、Work 與其他 domain-specific structures 屬於可擴充區段，類似 Rule Schema 的 extensibility：

| Extension                 | 可能內容                                                                   |
| ------------------------- | -------------------------------------------------------------------------- |
| **Scope Extension**       | Visible Scope、Artifact Scope、domain-specific Scope、parameterized Scope  |
| **Work Extension**        | activities、inputs、outputs、completion conditions、escalation conditions  |
| **Evidence Extension**    | required evidence、produced evidence、retention and grounding requirements |
| **Interaction Extension** | produces-for、escalates-to、separates-from 等關係與 contract               |
| **Capability Extension**  | Required Capabilities；Actor actual capability 仍在 binding 時判定         |

新的 extension type 可以事後加入，但必須明確、可解析、schema-governed、具版本與來源。Role Architecture 不預先封閉所有可能的 Scope 或 Work schema。

#### 3.3 Extension 的缺省語義

> **Extension 尚未提供，不代表無限制，也不授權模型自行補完。**

- Scope unresolved ≠ unrestricted Scope。
- Work unresolved ≠ 任意活動皆屬 Role 工作。
- Output Contract unresolved ≠ 任意輸出皆有效。
- Escalation unresolved ≠ 模型可以自行吸收未決問題。

未解析的 required extension 必須維持 `unresolved`，並在 binding 前補足、限制該 Role 的可用範圍，或觸發 escalation。

#### 3.4 Explicit Extension 與 Drift

- **Explicit Extension**：透過已宣告 extension point 加入，具有 identifier、schema、version、來源與相容性結果。
- **Contextual Binding**：在既有 extension schema 中解析此次 execution 的值。
- **Implicit Inference**：模型從上下文自行補出未宣告的 Scope、Work、Responsibility 或 Decision Right。

經由 Extension Schema 明確加入的是擴充；由模型自行補出、且沒有版本或 binding record 的改變是 drift candidate。

---

### 4. 核心物件

| 物件                | OO 類比                | 定義                                                                                                   |
| ------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------ |
| **Role Definition** | Class／Interface       | 持久、版本化、可解析的 Stable Core 與 extension declarations                                           |
| **Role Extension**  | Schema-governed module | 依宣告 extension point 附加的 Scope、Work、Evidence、Interaction 或 Capability structure               |
| **Binding**         | Instantiation          | 把 Role Definition 的特定版本、extensions 綁定到 Actor、model、flow、task context，可附帶明確 override |
| **Role State**      | Instance               | Binding 後的 contextual state；保留 CR canonical fields 與 binding metadata                            |
| **Actor**           | Implementation subject | 佔用 Role 的人、Agent 或 service；實際 capability 屬於 Actor／Role State                               |
| **Role Library**    | Package／Registry      | 管理 Role Definition、version、extension、dependency 與 compatibility metadata                         |

Role State 保留 Continuation Readiness 的 canonical fields：

> **Role State = {actor, viewpoint, policy, scope, authority, evidence-access, expected-output}**

Role Architecture 增加 Role Definition ID／version、model、flow、time、extensions 與 overrides 等 binding metadata；不是重新定義 Role State。

Prompt、system instruction、agent config、tool policy 與 output schema 都是 Role Definition／Binding 的 implementation artifacts，不是 Role meaning 的權威來源。

---

### 5. 可擴展：Specialization、Composition 與 Override

#### 5.1 Role Specialization

Role Specialization 建立 child Role Definition，但 child 是否可替代 parent 必須逐元素檢查。OO 只是類比，不代表 Role 可以任意 override。

> **A specialized Role may substitute for its parent only when every parent requirement remains satisfiable and every affected interface remains compatible.**

| 元素                  | 安全 specialization 原則                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Required Viewpoints   | 不可移除；新增 required viewpoint 必須證明不改變 parent consumer 所依賴的語義，否則建立 sibling／new major version |
| Constraint (MUST NOT) | 可新增；不可移除或放寬                                                                                             |
| Policy (MUST)         | 不可移除；新增不得與 parent Responsibility 或 contract 衝突                                                        |
| Responsibility        | child 必須自行保留 parent Responsibility；移轉給其他 Role 屬 composition／binding，不是 substitutability 例外      |
| Decision Right        | 不得因 specialization 自動擴張；擴張需獨立授權與新 Definition version                                              |
| Artifact Scope        | 可縮小；擴大不是安全替代，需新 version 或 sibling Role                                                             |
| Visible Scope         | 不得無條件擴大；擴張需符合 data authorization、parameterized Scope 與新版本／顯式 binding 規則                     |
| Input Contract        | 不得要求 parent consumer 無法提供的更強 precondition                                                               |
| Output Contract       | 只允許 receiver-compatible 的 covariance；必須通過 schema compatibility test                                       |

Responsibility transfer 可以形成新的 Role composition，但不能用來宣稱 child 仍完全替代 parent。

#### 5.2 Role Composition

Role Definition 以引用已版本化元件為主，不複製其內容：

```yaml
role: Technical-PM
extends: PM@1.0
extensions:
  viewpoint: architecture-awareness@1.0
  work: technical-pm-work@1.1
authority:
  application-ruleset: PM-TECH-RULESET@2.0
```

Role 不直接重新組裝 BRA atomic Rules。為維持 BRA 的 responsibility separation，Authority 應引用已組裝、版本化的 **Application Ruleset**；Role Library 管理 Role composition，不建立第二個 Rule composition authority。

若組合後同一條件下同時出現 `MUST X` 與 `MUST NOT X`，Role Definition 為 unsatisfiable，必須拒絕或交由具有適用 Decision Right 的治理程序解除。`MUST NOT` 可用於候選行為的 constraint-first 篩選，但不能藉由忽略 `MUST` 自動消除規則矛盾。

#### 5.3 Binding-time Override

Binding 可以在地化，但不能把未宣告推論偽裝成 override：

- Artifact Scope、Visible Scope 與 Decision Right 的改變必須符合 extension／binding schema；一般 binding 不得靜默擴張。
- Constraint 只可增加；移除需新 Definition version 與適用 Decision Right。
- Policy 不可靜默移除或矛盾化。
- Responsibility 縮減必須同時指定並取得 receiving Role 的 acceptance，否則形成 DR-V。
- Required extension unresolved 時，binding 必須拒絕、限制使用或 escalation。

Override record 至少包含 affected element、before／after value、basis、approving Decision Right、duration 與 receiving Role（若適用）。

#### 5.4 Evolution、Compatibility 與 Drift

三者分開判定：

- **Versioned Evolution**：Role Definition 有明確新版本、change basis 與 migration；可以是 breaking change。
- **Substitution Compatibility**：child 能否在需要 parent 的位置安全替代。
- **Role Drift**：Role meaning 在沒有相應 version、binding record 或 attribution 的情況下改變。

Substitution Rule 只判定 compatibility，不單獨決定 evolution 或 drift。

---

### 6. 可共享：Role Library

Role Library 是 Role Definition、Role Extension 與依賴關係的治理 registry。

- 共享單位具有 identifier、version、content identity 與 dependency manifest。
- 引用方必須 pin Role Definition 與重要 extension／Application Ruleset 版本。
- Stable Core 的改變必須升版，不能原地修改。
- Extension 的改變依 compatibility rule 判定是否需要 Role Definition 新版本。
- Role Library 引用 BRA Application Ruleset；不直接取代 BRA Rule Library。
- 跨組織共享時，共享物可為完整 Role Definition、parameterized Role template 或 abstract Role。

跨組織在地化不只涉及 Scope，也可能涉及 Authority、Decision Right、Responsibility、Evidence、ontology 與 legal context。所有在地化項目都必須透過 declared parameters、extensions 或 explicit binding 處理，不能複製後維持相同 identifier 各自修改。

---

### 7. Role Drift

**定義**：Role meaning 在沒有對應版本、明確 binding／extension record 或 attributable change 的情況下改變。

| Locus                | 說明                                                                          |
| -------------------- | ----------------------------------------------------------------------------- |
| **Definition Drift** | 同一 identifier／version 下 Stable Core 或 referenced extension identity 改變 |
| **Binding Drift**    | 實例化時發生未宣告、違反 schema 或超出 override 規則的改變                    |
| **Enactment Drift**  | 實際行為、輸出或 decision effect 超出 Role State                              |

Drift dimensions 可包括 Viewpoint、Responsibility、Authority、Decision Right、Scope、Work、Evidence 與 Interaction。

Role Drift 是缺少 Role Inference Boundary 或違反其 extension／binding rules 的主要可觀測症狀之一。v0.5 將工程化 Role Inference Boundary 與可擴展／可共享結構視為 architecture purpose，將 Drift 視為需要被預防與偵測的 failure condition。

---

### 8. 與既有研究的關係

| 構件                                        | 關係                                                                                                                            |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Engineering Determinacy**                 | 上位原則；已確立的 Role meaning 不應因 consuming model 改變而重新推論                                                           |
| **BRA**                                     | 提供 Authority 的 Policy／Constraint 與 Application Ruleset；Role Library 引用而不取代 Rule composition                         |
| **VSS**                                     | 提供 Viewpoint structure；viewpoint 不等於 Role，也不授予 Decision Right                                                        |
| **Boundary as an Execution-Time Primitive** | Task Execution Boundary 位於下游；Role Architecture 提供 Role 層宣告，不宣稱 Role label 缺失等於整體 execution boundary absence |
| **Scope as a Governance Primitive**         | Scope Extension 可引用 Visible、Artifact 或其他 viewpoint-dependent Scope                                                       |
| **DA／DR**                                  | 未承接的 Responsibility reduction 可造成 DR-V；超出 Decision Right 的 enactment 可造成 DR-O                                     |
| **Continuation Readiness**                  | Role State 保持 canonical 定義；Role Definition 與 Binding 提供其可重用來源                                                     |

---

### 9. 新穎性定位

> 本文不提出新的通用角色理論，而是提出 Role 在 LLM Agent 條件下的工程化形式：以 Role Inference Boundary 固定 Stable Core，並透過 schema-governed extensions、specialization、composition、binding 與 Role Library 支援明確擴充和共享。

| 前作                                | 已具備                                                                                  | 本文聚焦差異                                                                                                                  |
| ----------------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **RBAC／role engineering**          | permissions、hierarchy、constraints、SSD／DSD                                           | 不否定既有繼承與限制；增加 Viewpoint、Work、model binding 與 Role Inference Boundary                                          |
| **Gaia／MOISE+／OperA**             | structured roles、responsibilities、permissions／norms、activities／missions、protocols | 不宣稱其 Agent 必然 deterministic；聚焦 LLM context-based reconstruction、versioned extension 與 cross-model binding          |
| **Agent specifications／AgentCard** | identity、version、skills、capabilities、security／interface metadata                   | 不視為純 persona；指出其未必包含完整 Responsibility、Decision Right、Role specialization invariants 與 Role Library semantics |
| **BRA Rule Library**                | versioned atomic Rules 與 Application Ruleset composition                               | Role Library 是上層 Role assembly；只引用 Application Ruleset，不重做 Rule composition                                        |

---

### 10. 非目標

- 不建立新的 accountability 或責任歸屬理論；後果分析引用 DA／DR 與 Continuation Readiness。
- 不取代 Task Execution Boundary、runtime enforcement 或 tool permission。
- 不提出完整 Role relation algebra。
- 不提供量化 fidelity score。
- 不封閉所有 domain-specific Scope、Work 或 Evidence schema。

---

### 11. 開放問題

1. **Role Inference Boundary 的形式化**：如何判定 context-based interpretation 是否仍在 Role boundary 內？
2. **多重 specialization**：兩個 parent Role 的 Required Viewpoint、Responsibility 或 constraints 衝突時如何處理？
3. **Parameterized Scope**：跨組織共享時如何表示 Scope parameter 與 authorization？
4. **Extension compatibility**：哪些 extension change 可以不提升 Role Definition major version？
5. **Minimum completeness**：semantic completeness、bindable completeness 與 executable completeness 是否需要分層？
6. **Role relations**：`escalates-to`、`produces-for`、`separates-from` 是否足以作為最小集合？
7. **Inference evidence**：如何保留足夠證據證明模型對 Role 的實際理解，而不依賴不可觀察的 internal reasoning？


---

## 12. v0.6 修改目標

> 參照：`rule.schema.yaml`（dev-scr-rule-schema v1.0.0）

### 12.1 Schema 最小核心

**設計原則：** 對應 BRA rule schema 的精神——`normative` 是唯一強制行為欄位，其餘 governance 欄位全為選填延伸。Role Definition schema 應只強制最小的身份識別欄位，其餘一律歸入可擴展的 binding。

**必要欄位（四項）：**

| 欄位          | 說明                                               |
| ------------- | -------------------------------------------------- |
| `id`          | 唯一識別符，用於引用、版本比對、漂移追蹤           |
| `description` | 人類可讀的角色說明，為 binding 的語意錨點          |
| `version`     | 版本號，確保引用方知道綁定的是哪一個語意版本       |
| `status`      | 生命週期狀態（draft / active / deprecated 等）     |

其餘欄位（viewpoints、responsibilities、authority、scope、work、skills 等）**不在 required 列表中**，作為具名 binding 類型存在。導入企業可依治理需求自行新增 binding 類型。

### 12.2 Binding 可擴展性

新增 `skills` 為預定義 binding 類型：

| Binding 類型       | 說明                                                   |
| ------------------ | ------------------------------------------------------ |
| `viewpoints`       | 角色應從哪些專業視角解讀任務與回應                     |
| `responsibilities` | 角色負有哪些責任（聲明式，非 RBAC 的 permission 設定） |
| `authority`        | 角色的規則集與決策範圍（對應 BRA Authority 定義）      |
| `work`             | 角色應執行的工作定義與輸出合約                         |
| `scope`            | Visible Scope 與 Artifact Scope                        |
| `skills`           | 明確綁定至此角色的技能或能力單元（**新增**）           |

導入企業可自行新增額外 binding 類型（如 `risk_profile`、`data_classification`、`regulatory_scope`），不受 schema 約束。

### 12.3 Binding 類型的範例用途

Paper 應為每個預定義 binding 類型說明具體使用情境：

**`viewpoints`——Chat 回應視角**

在對話情境中，指定模型回應時應採用的專業視角。

> Role: PM，viewpoints: ["product strategy", "user value", "feasibility trade-off"]

當用戶詢問功能優先序，模型從產品策略與使用者價值角度回應，而非從工程技術或法規角度——同一「PM」標籤在不同 viewpoints binding 下產生不同回應邊界，這正是 Role Drift 問題的解方。

**`responsibilities` / `authority`——Agent Governance 稽核**

在 agentic flow 中，提供聲明式的權責邊界，作為**非 RBAC 的抽象授權層**，可供治理稽核使用。

> Role: Implementation Agent  
> responsibilities: ["write code", "run tests", "propose architecture"]  
> authority: MUST NOT merge to production branch without approval

稽核時比對 Evidence Record：Implementation Agent 選擇 caching strategy 是否超出 `responsibilities`（對應 DR-O）；直接 merge 是否違反 `authority` constraint（對應 Authority Drift）。無需 RBAC 的 permission 設定，仍可提供可稽核的授權語意。

**`skills`——明確技能綁定**

將特定 skill 單元明確綁定至角色，使技能可用性成為 Role Definition 的顯式宣告，而非 prompt 的隱含假設。

> Role: Code Reviewer  
> skills: ["anthropic-skills:code-review", "engineering:testing-strategy"]

- binding 時可驗證 skill 是否存在（Capacity check）；
- skill 升版時，引用此 Role Definition 的 binding 可追蹤能力邊界是否改變；
- 跨組織分享時，接收方可依 skill type/capability 做在地化對應。
