| 章節                   | 動作                       | 優先級 |
| ---------------------- | -------------------------- | ------ |
| Section 3 Anchor       | 完整形式化重寫             | 🔴 P0   |
| Section 5 Relationship | 加 R ⊆ A×A + 無語意陳述    | 🔴 P0   |
| Section 6 Views        | 每個加公式                 | 🔴 P0   |
| Section 7 Operations   | 每個加公式                 | 🔴 P0   |
| Section 4.3            | 加 Structural Decidability | 🟡 P1   |
| Section 3.3            | 加 Resolvability           | 🟡 P1   |
| Section 8 Example      | 展示推導能力               | 🟡 P1   |
| Introduction           | 加體系橋接                 | 🟡 P1   |
| Related Work           | 對比深化                   | 🔵 P2   |
| Conclusion             | 強化鋪墊                   | 🔵 P2   |


1. Anchor 是 artifact 的座標，以註解形式共存於 artifact 中，超輕量，零侵入，工具無關。這一句話應該在 Abstract 或 Introduction 就出現。這是整個架構最有說服力的特性之一。
2. Graph 應該改為 Topology，Set
3. 前面有定義過或表達過的 公式、表示式 和 範例，後面就不再重新出現
4. Anchor 不論程式或文件，一律 (ID, Location, version)
取代 FUNC-validate-password | src/auth/password.py | 1.4.0 這種表示式，感覺更像表示式
5. 程式只要註解，不需 
```python
def .....
```
6. 全部移除 Inference Creep, Ghost Intent, Decision Analysis, Decision Risk 等其他論文名稱