# 查經 Prompt Generator

> 🔥 為恩友堂 + ECF + 其他基督教小組組長而設嘅 Prompt 建構工具
>
> 基於 Hook-Book-Look-Took-Cook-Group（HBLTCG）+ OIA 查經法

---

## ❓ 呢個工具做咩？

組長每次帶查經前，都要用 AI（ChatGPT / Claude / Gemini / NotebookLM）整查經材料。
但係每次都要打長長嘅 prompt、記住一大堆規則（繁體中文、和合本、Cook 6W1H、組長先分享⋯⋯），好煩。

**呢個工具幫你一次過填表 → 自動產生**結構化嘅 prompt。你只要：
1. 填 30 秒 form（對象、時間、主題、特別要求）
2. Click「生成」
3. Copy prompt 去你用嘅 AI 平台
4. **另外自備經文同釋經材料**一齊交畀 AI

---

## 🎯 支援 3 個 AI 平台

| 平台 | 輸出 | 點用 |
|------|------|------|
| **General AI**（ChatGPT／Claude／Gemini） | 1 個長 prompt | 貼入對話框，paste 埋經文釋經 |
| **NotebookLM** | Instructions + Sources TXT | Instructions 貼入 NotebookLM 設定；TXT upload 去 Sources；另上傳經文釋經 |
| **Claude.ai Artifact** | 1 個 prompt | 貼入 Claude.ai，佢會建立 React 互動工作紙 |

---

## 📘 輸出 3 個版本

- **📘 組員版 Member Version**：標準 Markdown，問題冇答案
- **📗 組長版 Leader Version**：含建議答案、帶組貼士、組長先分享 Slot
- **📙 Interactive 組員版**：Markdown Checklist（或 Artifact HTML）

---

## 🙏 必備：組長 Pre-查 Prompt

《查經訓練》核心原則：**組長要先自己應用經文，然後才帶組員**。

本 Generator 可選「同時生成 Pre-查 Prompt」——組長查經前 1 週用呢個 prompt 同 AI 對話，AI 會用蘇格拉底式問題引導你：
1. 靜默讀經三次
2. 找出自己嘅 Took／Cook
3. 誠實寫低預計難處
4. 收集過往見證

查經當日，組長先分享呢啲內容，再邀請組員。**呢個係破 dead air、建立坦誠組內文化嘅關鍵**。

---

## 🚀 點用

### 方法 1：GitHub Pages（已部署）

直接去：`https://ivantheservant.github.io/chakeng/`（你自己 deploy 後嘅 URL）

### 方法 2：本地用

1. Clone／下載呢個 folder
2. `index.html`、`spec.md` 放同一 folder
3. 雙擊 `index.html` 打開（要 spec.md 喺同 folder，有啲 browser 可能會因為 CORS 阻擋 `file://` fetch，呢種情況下建議起 local server：`python -m http.server` 然後去 `localhost:8000`）

### 方法 3：部署去自己嘅 GitHub

見 `DEPLOYMENT_GUIDE.md`。

---

## 📂 檔案結構

```
chakeng-builder/
├── index.html              # Single Page UI
├── spec.md                 # Prompt templates（runtime fetch）
├── README.md               # 本檔案
└── DEPLOYMENT_GUIDE.md     # 部署指引
```

### 要改 prompt 邏輯？

只需改 `spec.md`，page refresh 就生效。唔需要改 HTML。

Section anchors：
- `RULES_COMMON`：共用規則（繁中、和合本、6W1H 等）
- `VERSION_BLOCK_MEMBER` / `_LEADER` / `_INTERACTIVE_MD`：三個版本嘅結構模板
- `PROMPT_GENERAL_BASE`：General AI 主 prompt
- `PROMPT_NOTEBOOKLM_INSTRUCTIONS`：NotebookLM Instructions (≤500 字)
- `PROMPT_NOTEBOOKLM_SOURCES_TXT`：NotebookLM Sources TXT
- `PROMPT_ARTIFACT_REACT`：Claude Artifact React
- `PROMPT_PREKUH`：組長 Pre-查

---

## 🧪 測試 Checklist

部署後／改完 spec 後，建議跑一次：

- [ ] General AI 平台 + 組員版 + 組長版 → 2 個 output
- [ ] NotebookLM 平台 → Instructions + Sources TXT
- [ ] Claude Artifact 平台 → 1 個 Artifact prompt
- [ ] 剔 Pre-查 → 多 1 個 Pre-查 Prompt output
- [ ] Copy 按鈕可用
- [ ] TXT 下載按鈕可用（只喺 NotebookLM 出現）

---

## 🎨 設計哲學

### 為何「Generator 唔處理經文／釋經材料」？

1. **釋經質素唔可以隨便**：AI 自己上網搵嘅釋經可能係異端／淺薄。組長必須用信得過嘅釋經書（如每日研經叢書、TheologAI MCP、教會提供嘅導讀）。
2. **Separation of concerns**：Generator 負責結構；組長負責內容。
3. **Copyright 友善**：我哋唔會把釋經書內容散佈出去。

### 為何強調「組長先應用先分享」？

引用《查經訓練.docx》p.5：
> 「組長的領受和分享：帶查經者能有領受，再能有效地與組員分享，就是最好的查經；也是鼓勵組員分享／破 dead air，很好的方法。」

呢個 pattern 係**破 dead air 最有效嘅技巧**，亦係將「教導式」查經變成「同行式」查經嘅關鍵。所以 Pre-查 Prompt 同「組長先分享」structural reminder 都係 v1.0 必備。

### 為何 Took vs Cook 分兩步？

- **Took**：原則性（「我要更愛主」）—— 容易講但容易流於空泛
- **Cook**：6W1H 具體化（「下週一朝 6:30 起身讀約翰一章，同 A 組員 WhatsApp 匯報」）—— 可執行、可量度、可守望

坊間好多查經只做到 Took。恩友堂堅持做到 Cook + Group 守望，呢個係本 Generator 嘅 DNA。

---

## 📣 致謝

- 查經方法論：恩友堂《查經訓練》（2024-25）
- OIA 框架：InterVarsity / Knowable Word / Salty Believer 等公開資源
- 產品設計：串嘴大叔 Ivan（@nononsensegospel）
- 技術實作：Claude (Anthropic) + Ivan 協作

---

**v1.0 · 2026-04-23**
