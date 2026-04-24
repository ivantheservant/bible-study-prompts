# 部署指引 Deployment Guide

查經 Prompt Generator — GitHub Pages 部署

---

## 📋 檔案清單

部署前確認呢 4 個檔案都齊：

- `index.html` — 主 UI（Single Page）
- `spec.md` — Prompt templates（runtime fetch）
- `README.md` — 用家簡介
- `DEPLOYMENT_GUIDE.md` — 本文件

---

## 🚀 部署步驟（GitHub Pages，約 10 分鐘）

### 步驟 1：建 GitHub Repo

1. 去 [github.com](https://github.com) 登入你個 `ivantheservant` account
2. 右上角 **+ → New repository**
3. Repository name：`chakeng`（或 `bible-study-prompts` 等你自己揀）
4. **Public**（GitHub Pages 免費版需要）
5. ✅ 剔 **Add a README file**（不過之後會被我哋嘅 README 覆蓋）
6. **Create repository**

### 步驟 2：Upload 檔案

**Option A：瀏覽器直接 Upload（最簡單）**

1. 新 repo 頁面，點 **Add file → Upload files**
2. 將 4 個檔案拖入：
   - `index.html`
   - `spec.md`
   - `README.md`
   - `DEPLOYMENT_GUIDE.md`
3. Commit message：`Initial commit - ChaKeng Prompt Generator v1.0`
4. **Commit changes**

**Option B：Git CLI**

```bash
git clone https://github.com/ivantheservant/chakeng.git
cd chakeng
# copy the 4 files here
git add .
git commit -m "Initial commit - ChaKeng Prompt Generator v1.0"
git push
```

### 步驟 3：開啟 GitHub Pages

1. Repo 頁面 → **Settings**（右上角 tab）
2. 左邊 sidebar → **Pages**
3. **Source**：`Deploy from a branch`
4. **Branch**：`main` + `/ (root)` → **Save**
5. 等 1-2 分鐘
6. 刷新頁面，頂部會顯示 URL：`https://ivantheservant.github.io/chakeng/`

### 步驟 4：驗證

1. 去 `https://ivantheservant.github.io/chakeng/`
2. 應該見到頁面載入
3. 開 Browser DevTools (F12) → Console，應該見到 `✅ spec.md loaded. Sections: [...]`
4. 填幾個欄位 → 按「生成 Prompt」→ 應該彈出 prompt

---

## 🧪 測試場景

用以下 test case 驗證部署成功：

**Test 1：General AI + 組員版 + 組長版**
1. §1 揀 General AI + 剔 組員版、組長版
2. §2 填：組名「恩友堂週五組」、10 人、青年、成長中、中、粵語
3. §4 填：經文「馬太福音 7:24-27」、主旨「聰明人與愚拙人建屋」
4. §5 填：組員處境「有弟兄近期失業」
5. §6 揀：故事、生活問題
6. §7 展開 → 剔「同時生成 Pre-查 Prompt」→ 填組長處境
7. 按「生成 Prompt」
8. 預期：2 個 output（General AI Prompt + Pre-查 Prompt）

**Test 2：NotebookLM**
1. §1 揀 NotebookLM
2. 其餘同 Test 1
3. 預期：3 個 output（Instructions + Sources TXT + Pre-查），Sources TXT 有「💾 .txt」下載按鈕

**Test 3：Claude Artifact**
1. §1 揀 Claude.ai Artifact
2. 其餘同 Test 1
3. 預期：2 個 output（Artifact Prompt + Pre-查）

---

## 🔧 日常維護

### 改 prompt 邏輯 → 只需改 `spec.md`

1. 喺 GitHub repo 頁面點 `spec.md` → 右上角鉛筆 icon 編輯
2. 改完 → 底部 **Commit changes**
3. 等 30-60 秒，刷新 Generator 頁面（Ctrl+Shift+R 強制 refresh 清 cache）
4. 即時生效

### 改 UI wording／配色 → 改 `index.html`

同上，編輯後 commit，等 30-60 秒。

---

## 🌐 URL 分享方式

部署成功後，分享以下 URL：

- 🔗 **給組長用**：`https://ivantheservant.github.io/chakeng/`
- 🔗 **其他教會用（唔需要改）**：同上（ECF 或其他教會組長亦可直接使用）

---

## ⚠️ 常見問題

**Q1：打開 URL 顯示「spec.md load failed」？**
- 確認 `spec.md` 同 `index.html` 喺同一 folder（repo root）
- 確認檔名大小寫一致（`spec.md`，唔係 `Spec.md` 或 `SPEC.md`）
- 開 F12 Console 睇詳細錯誤訊息

**Q2：改咗 spec.md 但 Generator 顯示舊內容？**
- Browser cache。按 `Ctrl+Shift+R`（Windows）或 `Cmd+Shift+R`（Mac）強制 reload
- 或等 5-10 分鐘 CDN cache 自動 refresh

**Q3：NotebookLM Instructions 生成後超過 500 字？**
- 編輯 `spec.md` 嘅 `## PROMPT_NOTEBOOKLM_INSTRUCTIONS` section，精簡內容
- 或喺 generator 填少啲背景資料，佢會內嵌入 Instructions

**Q4：想加新欄位／改預設值？**
- 改 `index.html`：加 form field + JS `collectFormData()` 對應讀取 + `buildPrompt()` 嘅 common map 填入
- 或叫我幫你改

---

## 🔄 更新到新版本

v1.x → v2.0 時：

1. 備份目前 `spec.md` 同 `index.html`（fork 一個 branch）
2. Upload 新版 4 個檔案覆蓋
3. Commit 訊息寫清楚版本號
4. 測試 Test 1/2/3

---

## 📞 聯絡

- 本 Generator 由串嘴大叔 Ivan 與 Claude 協作建立
- 問題／改進建議：透過本身嘅工作流（Claude Code / Claude Desktop）處理
- 建議 6 個月後按實際使用 feedback 迭代 v1.1
