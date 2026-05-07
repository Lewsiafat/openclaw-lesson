# OpenClaw Windows 課程實作計畫

日期：2026-05-07

---

## Goal

依照課程設計規格書，實作完整的互動式安裝教學網頁，
可直接部署到 GitHub Pages 供 1-on-1 線上教學使用。

## Architecture

```
openclaw-lesson/
  index.html            ← 單頁 wizard，包含 Step 0-9
  wizard.js             ← 通用步驟控制器（共用，不修改）
  style.css             ← Pico CSS 補充樣式（共用，不修改）
  screenshots/          ← 教學截圖（PNG）
  pre-class-checklist.md
  ai-runbook.md
  CLAUDE.md
  README.md
  docs/superpowers/
    specs/              ← 課程設計文件
    plans/              ← 實作計畫（本文件）
```

技術棧：
- Pico CSS v2（CDN）
- 零 build step
- `wizard.js` 從 `<body>` data attributes 讀取參數

## File Structure

| 檔案 | 用途 | 狀態 |
|------|------|------|
| `wizard.js` | 步驟切換邏輯 | 已完成（從 hermes 複製） |
| `style.css` | 樣式補充 | 已完成（從 hermes 複製） |
| `index.html` | 主要教學頁面 | 骨架已建立，內容待撰寫 |
| `CLAUDE.md` | 專案 AI 指令 | 已完成 |
| `README.md` | 專案說明 | 已完成 |
| `pre-class-checklist.md` | 課前驗證清單 | 已完成（結構） |
| `ai-runbook.md` | AI 截圖腳本 | 已完成（結構） |
| Spec 文件 | 課程設計規格 | 已完成 |
| Plan 文件 | 本文件 | 已完成 |

## Tasks

- [ ] **Task 0: Pre-implementation smoke check**
  - 在 Windows 環境驗證 `npm install -g openclaw` 是否仍可正常安裝
  - 確認 `openclaw --version` 輸出
  - 確認 `openclaw init` 互動流程
  - 記錄實際指令與輸出，用於填入教學內容

- [ ] **Task 1: Create index.html skeleton**
  - Step 0 + Steps 1-9 完整結構
  - 所有 `<section class="step">` 標記正確
  - 導覽按鈕可正常切換
  - `data-total-steps="9"` 和 `data-storage-key="openclaw-course-step"` 設定正確
  - **驗收：** 本地開啟，可用上一步/下一步瀏覽所有步驟

- [ ] **Task 2: Write Step 0 content**
  - OpenClaw 介紹（是什麼、能做什麼）
  - 與其他方案比較表（hermes-agent / nanobot / 直接用 ChatGPT）
  - 這堂課的目標與流程說明
  - **驗收：** 內容完整、排版正確

- [ ] **Task 3: Write Steps 1-4 content**
  - Step 1: 前置需求確認（含 winver 指令）
  - Step 2: Node.js 安裝（nvm-windows + 官方安裝程式雙路徑）
  - Step 3: OpenClaw CLI 安裝（含驗證指令）
  - Step 4: API Key 申請（OpenRouter 為主、備案說明）
  - 每步都有 `<pre data-copy>` 可複製指令
  - 每步都有 `<details>` 疑難排解區塊
  - **驗收：** 所有指令可複製、排版正確

- [ ] **Task 4: Write Steps 5-7 content**
  - Step 5: 初始化設定（openclaw init 流程）
  - Step 6: 第一次對話（openclaw chat 測試）
  - Step 7: Telegram 接通（BotFather → token → gateway）
  - **驗收：** 流程完整、指令正確

- [ ] **Task 5: Write Steps 8-9 content**
  - Step 8: 驗收清單（所有檢查項目）
  - Step 9: 加碼（Skills、其他平台、進階功能）
  - **驗收：** 驗收清單可勾選、加碼內容有吸引力

- [ ] **Task 6: Screenshots**
  - 依照 ai-runbook.md 進行完整截圖流程
  - 建立 `screenshots/` 目錄
  - 所有截圖統一 800px 寬
  - 命名遵循 `step-{N}-{描述}.png` 格式
  - **驗收：** 所有規劃截圖已產出

- [ ] **Task 7: pre-class-checklist.md**
  - 根據實際測試經驗，完善每個驗證步驟
  - 加入預期輸出與失敗時的處理方式
  - **驗收：** 講師可在 10 分鐘內跑完所有檢查

- [ ] **Task 8: ai-runbook.md**
  - Part 1: Full Capture Run（完整截圖腳本）
  - Part 2: Quick Smoke Test（快速驗證腳本）
  - 每個步驟有明確的操作與預期結果
  - **驗收：** AI 可照著腳本完成截圖

- [ ] **Task 9: Final smoke test + deploy**
  - 本地完整跑一次所有步驟
  - 確認所有連結、指令正確
  - Push 到 GitHub
  - 確認 GitHub Pages 部署成功
  - 更新 README 的「上次驗證」表格
  - **驗收：** Live URL 可正常存取
