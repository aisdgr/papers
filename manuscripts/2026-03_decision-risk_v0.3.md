# Decision Risk


## 1. Introduction — From Outcomes to Governance Effects**

本章說明本文的核心立場：  
**Decision Risk 是治理問題，而非工程正確性問題**。  
我們指出，隨著自動化與 AI 代理逐漸參與決策與執行流程，僅以產出結果（outcome correctness）作為分析依據已不足以揭示系統性風險。

本章強調：

- 本研究不評估程式是否「寫得對」
- 亦不試圖歸責個別錯誤
- 而是關注「決策如何被允許發生，以及是否可被事後取證」

並界定本文研究領域屬於 **governance**，  
軟體開發流程僅作為可觀測與可復現的分析場域。

---

## 2. Problem Framing — Over Outcome as an Observable Trigger**

本章引入 **over outcome** 作為分析起點，但非分類結果。

我們將 over outcome 定義為：

> 可觀察到的影響超出原先預期範圍的現象

並強調：

- over outcome 僅是「啟動治理分析的訊號」
- 不構成對錯判定
- 不預設任何治理失效

本章建立一個重要原則：  
**治理分析不從原因假設開始，而從現象顯化開始。**

---

## 3. Governance Boundary Conditions — Scope Drift and Inference Creep**

本章說明兩種必須**優先排除**的治理現象：

- **Scope Drift**：分析前提（輸入／輸出範圍）本身已失效
- **Inference Creep**：推論語義或目標在未被顯化的情況下擴張

這兩者若成立，將直接使後續決策分析失去基準。

本章的關鍵貢獻在於：

- 將 Scope 與 Inference 明確區分
- 指出它們是 **治理前提問題，而非決策問題**
- 建立「先排除、再歸因」的判定順序

---

## 4. Decision Authority Effect (DAE) — Making Authority Observable**

本章引入 **Decision Authority Effect (DAE)**，作為 v0.3 的關鍵穩定基底。

DAE 被定義為：

> 某一權限配置在實際執行中所產生的可觀測影響集合

本章刻意不討論：

- 權限是否合理
- 決策是否正確
- 治理是否失敗

而僅關注：

- 哪些行為實際被啟用
- 哪些影響面實際被打開
- 這些效果是否可被取證與重建

DAE 提供了一個**非主觀、非規範**的中介層，使後續治理判定具備可防守的觀測基礎。

---

## 5. Decision Risk Taxonomy — Interpreting Effects Without Normative Judgement**

本章在 DAE 的基礎上，提出 **Decision Risk 的分類學**，而非評價學。

三類 Decision Risk 被定義為：

- **DR-V (Decision Vacancy)**  
    權限效果存在，但無任何可歸屬的決策記錄
- **DR-O (Over Decision Risk)**  
    權限效果可歸屬，但其影響面顯著過寬或不可收斂
- **DR-I (Indeterminate Decision Risk)**  
    權限效果存在，但證據不足以支持任何治理判定

本章強調：

- Decision Risk 不是錯誤分類
- 而是「治理不可確定性與結構性風險」的標記

---

## 6. Reproducibility and Evidence Completeness**

本章說明 Decision Risk 判定所需的最小可復現條件，包括：

- 決策輸入範圍（input scope）
- 決策輸出範圍（output scope）
- 權限配置記錄
- 執行命令與過程軌跡
- 產出差異（artifact diff）

同時指出：

- 證據不完備本身即是一種治理風險
- 不可判定性（indeterminacy）不等於分析失敗

---

## 7. Discussion — Governance Without Outcome Dependence**

本章討論本文方法論的治理意涵。

重申三個核心立場：

1.  Decision Risk 與產出正確性不存在可量化對應關係
2.  治理分析應建立在可觀測效果，而非事後價值判斷
3.  軟體工程是治理取證的媒介，而非研究終點

並說明此框架如何避免：

- outcome-based blame
- post-hoc drift judgement
- governance overreach

---

## 8. Conclusion — From Decision Judgement to Effect-Based Governance**

結論章總結本文的核心貢獻：

- 將 Decision Risk 從主觀治理判斷，轉化為基於可觀測效果的取證流程
- 提供一套可復現、可防守的治理分析方法
- 為後續更形式化的治理架構奠定基礎

本章亦指出未來工作將聚焦於：

- effect 表示法的標準化
- 不同自動化場域的適用性分析
- Decision Risk 與制度設計之間的關係
