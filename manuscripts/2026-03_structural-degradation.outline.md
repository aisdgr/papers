# Structural Degradation: From Stateless Generation to Layered Software Decay in AI-Generated Code
> A Three-Layer Taxonomy of Software Decay and Its Governance Implications

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  

---

# Abstract
- 目的:概括論文的研究問題、方法、發現和價值
- 重點:參考v0.3的Abstract,提煉以下要點:
    | 要素 | 內容                                                                                                                  |
    | ---- | --------------------------------------------------------------------------------------------------------------------- |
    | 背景 | AI生成代碼引入Structural Mismatch:Stateless生成vs Stateful演化                                                        |
    | 缺口 | 現有討論聚焦Hallucination, Defect, Productivity,缺乏對獨特Degradation Mechanism的統一解釋                             |
    | 方法 | 提出Three-Layer Degradation Taxonomy (Intent, Structural, Behavioral)                                                 |
    | 發現 | 識別14種Degradation Phenomena,揭示其共同Root Cause (Stateless vs Stateful Mismatch)和Cross-Layer Propagation Dynamics |
    | 意義 | 建立Degradation Pattern的連貫Ontology,為未來Research奠定Foundation                                                    |

---

## Keywords
- 目的:列出5-7個最能體現論文核心內容和貢獻的關鍵詞
- 重點:圍繞v0.3的核心概念,突出以下關鍵詞:
  - AI-Generated Code
  - Structural Degradation
  - Stateless Generation  
  - Stateful Evolution
  - Three-Layer Taxonomy
  - Cross-Layer Dynamics
  - AI-Assisted Software Engineering  

---  

## JEL Classification
- 目的:按照Journal of Economic Literature (JEL)分類系統,標明論文所屬的研究領域和主題
- 重點:對照JEL分類,本文主要涉及:  
  - C88 - Design of Experiments: Software Engineering
  - O33 - Technological Change: Choices and Consequences 
  - M15 - IT Management

---

## 1. Introduction
- 目的:引出研究問題,解釋研究動機,概述研究方法和貢獻
- 重點:參考v0.3的Central Thesis,圍繞以下邏輯展開:
  1. AI-Generated Artifact引入Structural Mismatch:Stateless Output vs Stateful System  
  2. 該Mismatch在Intent, Structural, Behavioral三個Abstraction Layer產生Degradation Pattern
  3. 這些Pattern在當前Software Engineering Discourse中Remain Under-Theorized
  4. 本文構建Three-Layer Taxonomy,系統定義14種Degradation Phenomena
  5. 研究揭示這些Phenomena的Common Root Cause和Cross-Layer Propagation Dynamics
  6. 研究為未來Analytical, Governance, Architectural Work提供必要Conceptual Foundation

---

## 2 Structural Degradation 
- 目的:界定核心概念,闡明研究視角
- 重點:參考v0.3的定義,從以下角度界定Structural Degradation:
    | 角度 | 闡釋                                                                              |
    | ---- | --------------------------------------------------------------------------------- |
    | 本質 | AI Generated Code引入的Structural Mismatch所導致的Architecture Decay              |
    | 表現 | 體現為Intent, Structural, Behavioral三個Layer的Degradation Phenomena              |
    | 根源 | 源於Stateless Generation和Stateful Evolution之間的Three-Dimensional Discontinuity |
    | 區別 | 不同於Bug, Technical Debt, Dead Code等Localized, Isolated缺陷                     |
    | 機制 | 通過Cross-Layer Propagation Dynamics傳播,呈現Cascading, Intertwined的Degradation  |

---

## 3 Root Cause: Stateless Generation vs Stateful Evolution
- 目的:剖析問題根源,構建因果分析框架
- 重點:參考v0.3的1. Root Cause部分,闡述以下Causal Logic:
    | 因                                                                                                  | 果                                                                                                                                                                    |
    | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | 傳統SDLC假設:Persistent Authorship, Incremental Evolution, Boundary-Respecting Modification         | 支撐Cumulative System Growth                                                                                                                                          |
    | AI Generation打破假設,引入Three-Dimensional Discontinuity                                           | 導致Integration變得Non-Cumulative                                                                                                                                     |
    | Temporal Discontinuity:Isolated Completion, Lack of Persistent Historical Awareness                 | Regeneration Partially Resets Local Structure                                                                                                                         |
    | Authorial Discontinuity:Dispersed Authorship across Probabilistic Outputs & Transient Prompts       | Artifacts Lack Recoverable Authorial Continuity                                                                                                                       |
    | State Discontinuity:Generation Treats System as Snapshot, Ignores Implicit Constraints & Invariants | Integration Violates Accumulated Architectural Assumptions                                                                                                            |
    | Three-Dimensional Discontinuity Co-Existence                                                        | 使Integration Non-Cumulative,Repeated Structural Resets取代Extending Prior Structure;Degradation Emerges from Resets Embedded in Evolving System,而非Isolated Defects |

---

## 4 A Three-Layer Taxonomy of Structural Degradation
- 目的:在Three-Layer框架下系統定義和描述Degradation Phenomena
- 重點:參考v0.3的Intent, Structural, Behavioral Layer Degradation部分,對每個現象從以下維度展開:  
    | Layer      | Phenomena                     | Definition                       | Distinction                                   | Example                                       | Path Logic                            |
    | ---------- | ----------------------------- | -------------------------------- | --------------------------------------------- | --------------------------------------------- | ------------------------------------- |
    | Intent     | Ghost Intent                  | 源Decision不可復原的執行Artifact | vs Undocumented, Missing Requirement          | 性能優化需求缺失下的Caching Logic             | Static Absence                        |
    | Intent     | Inference Creep               | 生成超出Instruction Boundary     | vs Hallucination, Bug, Scope Creep            | -                                             | Probabilistic Overreach               |
    | Intent     | Semantic Expansion            | 生成過程中概念外延擴大           | vs Prompt Drift, Misunderstanding             | Validate→ Sanitize, Normalize, Transform      | Beyond Declared Meaning               |
    | Intent     | Fragmentation                 | Intent存在但結構分散             | vs Ghost Intent:Presence vs Absence           | -                                             | Origin Present, Cohesion Absent       |
    | Intent     | Scope Absorption              | 隱式吸收鄰近Concern              | Boundary Swallowing vs Crossing               | -                                             | Implicit Inclusion                    |
    | Intent     | Drift                         | 跨Iteration漸進偏離              | vs Deliberate Modification                    | Local Regen Optimizes without Original Anchor | Gradual Deviation                     |
    | Intent     | Collision                     | 跨Agent/Iteration的Intent衝突    | -                                             | -                                             | Conflicting Direction                 |
    | Structural | Ghost Code                    | 目的不確定的Code                 | vs Dead Code:Executable vs Unreachable        | -                                             | Interpretability Indeterminate        |
    | Structural | Architectural Amnesia         | 衝突的隱式架構模型並存           | -                                             | -                                             | Conflicting Mental Models             |
    | Structural | Rigidity Calcification        | 無意識的模式固化降低可演化性     | vs Tech Debt:Unconscious vs Conscious         | -                                             | Cumulative Pattern Uniformity         |
    | Structural | Shadow Coupling               | 隱式依賴路徑                     | -                                             | -                                             | Undeclared Dependencies               |
    | Structural | Interface Erosion             | 漸進邊界模糊                     | -                                             | -                                             | Incremental Boundary Blurring         |
    | Structural | Dependency Blindness          | 隱式外部依賴直到失效才浮現       | -                                             | 生成物假設API響應順序,版本變化無聲打破        | Fragile Implicit Assumptions          |
    | Behavioral | Conditional Blindspot         | 系統性遺漏稀有邊界Case           | vs Random Bug:Bias Correlates with Generation | -                                             | Omission Bias                         |
    | Behavioral | State Assumption Leak         | 特定序列下隱式State假設失效      | -                                             | -                                             | Sequence-Dependent Violation          |
    | Behavioral | Observation Bias              | 監控與預期行為相關,忽略異常      | vs Incomplete Logging, Random Gap             | -                                             | Expectation-Driven Monitoring         |
    | Behavioral | Non-Deterministic Degradation | 非局部Bug,行為非穩定正確/錯誤    | -                                             | -                                             | Load & Sequence Dependent Instability |
    | Behavioral | Confidence Propagation        | 儘管假設降級,系統仍表達Certainty | -                                             | -                                             | Suppressed Error Signals              |

---  

## 5 Cross-Layer Degradation Dynamics
- 目的:闡明Degradation Phenomena的Cross-Layer Dynamics和Propagation Mechanisms
- 重點:參考v0.3的5. Cross-Layer Dynamics部分,說明以下Propagation Logic:
    | Dynamics                                    | Mechanism                                                                                                                                              |
    | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | 主要方向:Intent → Structural → Behavioral   | Abstraction Loss易於Abstraction Reconstruction;一旦Intent Instability嵌入Structure,恢復Original Context指數級困難                                      |
    | Intent → Structural                         | Inference Creep(Scope Absorption) → Absorbed Logic Standardizes into Templates(Rigidity Calcification) → Rigid Templates Prevent Adaptation Under Load |
    | Structural → Behavioral                     | Shadow Coupling → Hidden State Dependency → State Assumption Leak Under Stress → Repeated Leaks → Non-Deterministic Degradation                        |
    | Behavioral → Structural/Intent (Diagnostic) | Behavioral Failure揭示Structural/Intent Issue;Diagnostic而非Causal,Behavioral Intervention無法逆轉Upstream Degradation                                 |
    | Visibility Inversion                        | 檢測概率 ∝ 1/Generation Layer Depth, 損害幅度 ∝ Failure Layer Depth;Intent Issue Early Detection Cheap, Behavioral Failure Late & Costly               |

---

## 6 Visibility Inversion Principle
- 目的:系統闡述Visibility Inversion Principle及其Governance啟示
- 重點:在v0.3的Cross-Layer Dynamics基礎上,深入闡明以下內涵:
    | 內涵     | 闡釋                                                                                 |
    | -------- | ------------------------------------------------------------------------------------ |
    | 檢測難度 | 與Generation時的Layer Depth成反比:Behavioral Failure易見,Intent Issue難察            |
    | 損害幅度 | 與Failure時的Layer Depth成正比:Behavioral Failure損害大,Intent Issue損害小           |
    | 治理啟示 | Governance成本隨Depth增加;需儘早檢測Intent Issue;需Cross-Layer追溯Failure Root Cause |
    | 架構啟示 | 需Mechanism顯式化Deep Layer狀態;需架構支持Cross-Layer Tracking/Tracing               |
    | 過程啟示 | 需在Shallow Layer引入Verification;需將Degradation監控嵌入CI/CD                       |

---

## 7 Implications for Software Engineering
- 目的:探討研究對Software Engineering的啟示
- 重點:結合v0.3的Root Cause, Layered Taxonomy, Cross-Layer Dynamics,提出以下Implications:
  1. 統一Ontology:Three-Layer Taxonomy為描述AI Degradation提供連貫概念框架,揭示傳統Defect Taxonomies局限 
  2. 診斷導向:Stateless vs Stateful引發的Three-Dimensional Discontinuity視角,指引識別和預防Degradation Root Cause
  3. 架構革新:需適應AI Generated Artifact的新架構原則(Isolate Non-Cumulative Integration, Explicit Evolution Constraint, Dynamic Authorial Traceability等)  
  4. 治理重塑:需Cross-Layer追溯Degradation路徑,結合動靜態分析,構建Observability,聚焦Intent Layer Early Detection
  5. 過程優化:需在SDLC中引入新活動(Generated Artifact Consistency Audit, Explicit Architecture Assumption Validation, Periodic Degradation Assessment等)

---

## 8 Limitations
- 目的:反思局限性,明確未來研究方向
- 重點:參考v0.3的6. Limitations,提出以下局限和展望:
  - Conceptual而非Empirical Taxonomy,尚需實證驗證
  - 某些Intent層概念邊界可能模糊,有待進一步細化  
  - 假設Artifact Integration發生在Long-Lived Evolving Systems中,對Short-Lived/Disposable Systems的適用性有待探索
  - 尚無Quantitative Measurement,未來需發展Degradation度量體系
  - 尚未觸及Prevention和Mitigation Mechanism Design,有待後續研究  

---

## 9 Conclusion
- 目的:總結全文,重申貢獻,展望未來
- 重點:參考v0.3的7. Contribution,圍繞以下要點收尾:  
  1. 針對AI-Generated Code Degradation,提出基於Three-Dimensional Discontinuity的Root Cause Model
  2. 構建跨Intent-Structural-Behavioral三層的Degradation Taxonomy,系統定義14種Phenomena
  3. 闡明Degradation的Cross-Layer Propagation Model,揭示Visibility Inversion Principle  
  4. 在概念上區分Structural Degradation與Bug, Technical Debt, Dead Code等傳統概念
  5. 強調只有在Layered Ontology框架下,才能準確把握AI Degradation,避免Misclassification導致Misaligned Remediation
  6. 未來將圍繞Empirical Analysis, Phenomenon Expansion, Governance Framework, Process Guidance等開展深入研究

---

## 10. Related Work
- 目的:梳理文獻脈絡,凸顯本研究的獨特貢獻
- 重點:參考v0.3的Reference,在更多AI Engineering文獻基礎上,系統比較本研究與以下方向的區別和聯繫:
    | 研究方向                         | 代表文獻     | 本文貢獻                                                     |
    | -------------------------------- | ------------ | ------------------------------------------------------------ |
    | AI-Assisted Software Engineering | [1][2][3]    | 聚焦Structural Degradation而非General Quality                |
    | Software Architecture Decay      | [4][5][6]    | 引入AI-Generated Code Perspective                            |
    | Technical Debt Management        | [7][8][9]    | 超越單一Technical Debt概念,刻畫Multi-Layer Debt Dynamics     |
    | Software Evolution Governance    | [10][11][12] | 提出針對AI Artifact的Stateless-Aware Governance框架          |
    | AI Testing and Verification      | [13][14][15] | 從Structural Degradation視角揭示新的Testing/Verification需求 |

## References
- 目的:全面梳理支撐性文獻,奠定研究的理論基礎
- 重點:在v0.3的Reference基礎上,補充更多與本研究直接相關的經典文獻和前沿成果,初步擬包括:
  - Parnas, D. (1972). On the Criteria To Be Used in Decomposing Systems into Modules.
  - Brooks, F. (1975). The Mythical Man-Month.
  - Belady, L. & Lehman, M. (1976). A Model of Large Program Development.
  - Cunningham, W. (1992). The WyCash Portfolio Management System (Technical Debt).
  - Gruber, T. (1993). A Translation Approach to Portable Ontologies.
  - Coplien, J. (1996). Software Patterns: Gardening and the Concept of Design Debt.
  - Li et al. (2015). A Systematic Mapping Study on Technical Debt and Its Management.
  - Shumailov et al. (2023). The Curse of Recursion.
  - Abbassi et al. (2025). Taxonomy of Inefficiencies in LLM Code.
  - Shukla et al. (2025). Security Degradation in AI Code Generation.
