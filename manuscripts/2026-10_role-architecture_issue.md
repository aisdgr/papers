# Role Architecture — Concept Issues

## v0.5

| 項目     | 內容                                               |
| -------- | -------------------------------------------------- |
| 日期     | 2026-10-25                                         |
| 檢核對象 | `2026-10_role-architecture_concept.md` v0.5        |
| 狀態     | Concept 已依確認基準修訂；保留項目待後續研究或決策 |

---

### 已確認並納入 Concept

- [x] **Boundary 類型已釐清。** Role Architecture 建立的是 **Role Inference Boundary**，不是 Task Execution Boundary。Role Definition 約束模型如何理解 Role；Role State 與 task context 再參與下游 Execution Boundary 的解析。

- [x] **Boundary absence 已收斂。** 只有 Role label 代表 Role Inference Boundary 缺失，不代表整個 Task Execution Boundary 必然不存在。

- [x] **核心情境已建立。** Prompt 與 flow 中若沒有獨立 Role Definition，Role meaning 由 user task、system prompt、history、retrieval、tools、workflow position 與上下游輸出共同推論，可能形成 Role Drift 與 Implicit Decision-Right Expansion。

- [x] **Agentic flow 對照已改為風險放大條件。** 不再宣稱單次 prompt 必然有人修正、只輸出文字或不受 model replacement 影響。

- [x] **Role Definition 已改為 Stable Core + Extension Sections。** Stable Core 固定 Identity、Version、Description、Required Viewpoints、Responsibilities、Authority、Decision Rights 與 Extension Declarations；Scope、Work、Evidence、Interaction、Capability 可由 schema-governed extensions 擴充。

- [x] **Extension 缺省語義已確立。** Extension unresolved 不等於 unrestricted，也不得由模型自行補完；binding 必須補足、限制使用或 escalation。

- [x] **Responsibility 與 Decision Right 已納入 Stable Core。** 不再假設 Policy 等同 Responsibility，也不以 Constraint 代替決策權。

- [x] **Role State 已保留 Continuation Readiness canonical fields。** Actor、model、flow、time、extensions 與 overrides 被定位為新增 binding metadata，不改寫 Role State。

- [x] **Behavior Space 已從 Concept 核心公式移除。** Scope Extension 可以引用既有 Scope constructs，但不再把 `Artifact Scope × Authority` 表述為既有 canonical 公式。

- [x] **Role Specialization 規則已收緊。** 新增 Viewpoint、擴張 Visible Scope、Responsibility transfer 與 Output Contract change 都必須經 compatibility 判定，不能視為無條件安全 subtype。

- [x] **Evolution、substitution 與 drift 已分離。** Versioned breaking change 可以是 governed evolution；Substitution Rule 只判定 child／parent compatibility；Drift 仍依 version、binding record 與 attribution 判定。

- [x] **直接規則衝突不再以 MUST NOT 自動覆蓋 MUST。** 同條件的矛盾規則使 composition unsatisfiable；constraint-first 只用於候選行為篩選。

- [x] **CFGA 依賴已移除。** 在 workspace 中沒有 canonical artifact 前，不再把 CFGA 當成既有依據。

- [x] **Role Library 與 BRA responsibility 已分離。** Role Definition 引用 BRA Application Ruleset；Role Library 不直接重新組裝 atomic Rules。

- [x] **跨組織共享已擴充。** 在地化不限於 Scope，也涵蓋 Authority、Decision Right、Responsibility、Evidence、ontology 與 legal context；共享物可為完整 Definition、parameterized template 或 abstract Role。

- [x] **Prior-work 描述已收斂。** 不再把 AgentCard 等同純 persona、不再宣稱 Gaia／MOISE+ 必然採 deterministic Agent，也不再忽略 RBAC hierarchy、constraints 與 SSD／DSD。

- [x] **v0.5 thesis change 已明示。** Role Drift 保留為重要 failure condition，但 architecture purpose 改為 Role Inference Boundary 工程化與 Role 的可擴展／可共享結構；此變動需要在後續 manuscript history 記錄為 thesis refocusing。

### 待後續確認

- [ ] **Role Inference Boundary 的可觀測判準。** Role Definition 可外部化 established meaning，但模型實際如何理解 Role 仍不能直接觀察。待定義可接受的 output／action／evidence proxy，避免要求保留 internal chain-of-thought。

- [ ] **三層 completeness。** 待確認是否正式區分 semantic completeness、bindable completeness 與 executable completeness，以及各自必需的 Stable Core／Extension elements。

- [ ] **Extension version propagation。** 待確認 Scope／Work／Evidence extension 的 compatible update 是否必須提升 Role Definition version，或只更新 dependency lock／manifest。

- [ ] **多重 specialization。** 待定義 parent Role 之間 Viewpoint、Responsibility、Authority、Decision Right 與 contract 衝突的檢測及拒絕規則。

- [ ] **Parameterized Scope authorization。** 待定義 template parameter 的允許範圍、誰可賦值，以及參數化 Scope 如何與實際 data／artifact permission 對接。

- [ ] **最小 Role relation 集合。** 待驗證 `produces-for`、`escalates-to`、`separates-from` 是否足以支援 Role composition，而不重新引入完整 workflow algebra。
