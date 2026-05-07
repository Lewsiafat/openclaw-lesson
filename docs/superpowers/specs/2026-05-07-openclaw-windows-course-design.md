# OpenClaw Windows 安裝課程設計規格書

日期：2026-05-07

---

## 1. 摘要

一堂 60 分鐘的線上 1-on-1 課程，帶 Windows 使用者從零開始安裝 OpenClaw AI Agent 框架，
完成第一次對話，並接通 Telegram 作為訊息介面。

課程以互動式網頁（wizard）引導，學員跟著步驟操作，講師即時排除問題。

## 2. 目標與終點

課程結束時，學員擁有：

1. 一台已安裝 Node.js 22+ 與 OpenClaw CLI 的 Windows 電腦
2. 一組可用的 AI API Key（OpenRouter / Anthropic / OpenAI 擇一）
3. 已完成 `openclaw init` 初始化設定
4. 成功與 OpenClaw agent 進行至少一次文字對話
5. 已接通 Telegram bot，可透過 Telegram 與 agent 互動
6. 知道如何查看 health check、重啟 agent、尋找文件

## 3. 對象與預設

### 學員特徵
- 使用 Windows 11 的一般使用者（有基本命令列經驗更佳）
- 對 AI / ChatGPT 有興趣，想要自架 agent
- 不一定有程式開發經驗，但願意跟著指令操作
- 已有 Telegram 帳號

### 預設環境
- Windows 11（22H2 或更新）
- 穩定網路連線
- 管理員權限（能安裝軟體）
- 瀏覽器（用於申請 API Key）

### 與 hermes 課程的差異
- OpenClaw 原生支援 Windows，不需要 WSL2（大幅簡化）
- 需要安裝 Node.js（hermes 需要 Docker Desktop）
- API Key 需要自行申請（hermes 可能內建試用額度）
- 目標學員可以稍具技術背景

## 4. 範圍

### In Scope
- Node.js 22+ 安裝（nvm-windows 或官方安裝程式）
- OpenClaw CLI 全域安裝
- API Key 申請流程（OpenRouter 為主，Anthropic/OpenAI 為備案）
- 初始化設定（`openclaw init`）
- 第一次對話驗證
- Telegram bot 接通
- 基本 health check 與驗收

### Out of Scope
- Linux / macOS 安裝
- Docker 部署方式
- 自訂 Skills 開發（僅預覽）
- 多平台同時接通（僅 Telegram）
- 程式碼層面的客製化

### Optional（時間允許才做）
- OpenClaw Skills 功能簡介
- 其他平台接通預覽（Discord, WhatsApp）
- 設定檔進階調整

## 5. 課程時間表（60 分鐘）

| 時間 | 分鐘 | 講師活動 | 學員活動 | 對應步驟 |
|------|------|----------|----------|----------|
| 0:00 | 3 | 自我介紹、課程目標說明 | 確認螢幕分享、開啟課程頁面 | Step 0 |
| 0:03 | 2 | 說明前置需求 | 確認 Windows 版本、管理員權限 | Step 1 |
| 0:05 | 8 | 引導安裝 Node.js | 下載並安裝 Node.js 22+ | Step 2 |
| 0:13 | 5 | 引導安裝 OpenClaw CLI | 執行 `npm install -g openclaw` | Step 3 |
| 0:18 | 8 | 說明 API Key 用途、引導申請 | 註冊 OpenRouter 並取得 Key | Step 4 |
| 0:26 | 7 | 引導初始化設定 | 執行 `openclaw init`，填入 API Key | Step 5 |
| 0:33 | 5 | 引導第一次對話 | 與 agent 聊天、確認回覆正常 | Step 6 |
| 0:38 | 10 | 引導 Telegram 接通 | 建立 bot、設定 token、啟動 gateway | Step 7 |
| 0:48 | 5 | 引導驗收 | 從 Telegram 發訊息、確認 agent 回覆 | Step 8 |
| 0:53 | 5 | 展示進階功能 | 觀看、提問 | Step 9 |
| 0:58 | 2 | 總結、提供後續資源連結 | 記下重點 | — |

### 講師注意事項
- Node.js 安裝通常最耗時（下載 + 安裝精靈），預留充足時間
- API Key 申請可能需要信用卡驗證，事先提醒學員準備
- Telegram bot 建立流程較直覺，但 token 複製容易出錯

## 6. 教學網頁設計（Wizard）

### 技術選擇
- Pico CSS（CDN，無需 build）
- 共用 `wizard.js`（與 hermes-windows-course 相同）
- 單一 `index.html` 包含所有步驟

### Wizard 參數
```html
<body data-total-steps="9" data-storage-key="openclaw-course-step">
```

### 互動元素
- 每個步驟有 `<pre data-copy>` 的可複製命令區塊
- `<details>` 折疊區塊用於「遇到問題？」疑難排解
- 導覽列顯示目前進度、上一步 / 下一步按鈕

### 截圖規範
- 寬度：統一 800px
- 格式：PNG
- 命名：`screenshots/step-{N}-{描述}.png`
- 內容：實際 Windows 畫面截圖，標註重要區域

## 7. 安裝步驟規劃

### Step 0：前言

**目標：** 讓學員理解為什麼選擇 OpenClaw、它能做什麼。

內容要點：
- OpenClaw 是什麼（TypeScript/Node.js AI agent 框架）
- 為什麼選 OpenClaw（開源、50+ 平台整合、原生 Windows 支援）
- 與其他方案比較表（hermes-agent、nanobot、直接用 ChatGPT）
- 這堂課會做到什麼（安裝 → 對話 → 接通 Telegram）

### Step 1：確認前置需求

**目標：** 確保學員環境符合最低要求。

檢查項目：
- [ ] Windows 11（22H2+）
- [ ] 管理員權限
- [ ] 穩定網路（需下載 ~100MB）
- [ ] 瀏覽器（Chrome / Edge）
- [ ] Telegram 帳號

驗證指令：
```
winver
```

### Step 2：安裝 Node.js 22+

**目標：** 安裝 Node.js LTS（>= 22.14）。

兩條路徑：
1. **推薦：nvm-windows**（方便日後管理多版本）
   ```
   # 先下載 nvm-windows installer
   # https://github.com/coreybutler/nvm-windows/releases
   nvm install 22
   nvm use 22
   ```
2. **備案：官方安裝程式**
   - 下載 https://nodejs.org/ LTS 版本
   - 執行安裝精靈，全部預設

驗證：
```
node --version
npm --version
```

預期結果：`v22.x.x` 以上

### Step 3：安裝 OpenClaw CLI

**目標：** 全域安裝 OpenClaw。

指令：
```
npm install -g openclaw
```

驗證：
```
openclaw --version
```

常見問題：
- 權限不足 → 以系統管理員開啟 PowerShell
- npm 版本過舊 → `npm install -g npm@latest`

### Step 4：申請 API Key

**目標：** 取得至少一組 AI API Key。

推薦順序：
1. **OpenRouter**（最簡單，支援多模型）
   - 前往 https://openrouter.ai/
   - 註冊帳號
   - 建立 API Key
   - 儲值少量金額（$5 即可）
2. **Anthropic**（直連 Claude）
   - https://console.anthropic.com/
3. **OpenAI**（直連 GPT）
   - https://platform.openai.com/

**重要：** 複製 API Key 後立即貼到安全的地方（記事本），頁面關閉後無法再看。

### Step 5：初始化設定

**目標：** 完成 OpenClaw 初始化。

指令：
```
openclaw init
```

設定過程中需要填入：
- AI provider（選擇 OpenRouter / Anthropic / OpenAI）
- API Key（貼上 Step 4 取得的 Key）
- Agent 名稱（可隨意取）
- 其他設定保持預設

驗證設定檔已建立：
```
openclaw config show
```

### Step 6：第一次對話

**目標：** 確認 agent 能正常回覆。

指令：
```
openclaw chat
```

測試對話：
- 「你好，請自我介紹」
- 「今天天氣如何？」（測試是否能回覆）
- Ctrl+C 結束對話

成功標準：agent 能用中文回覆完整句子。

### Step 7：接通 Telegram

**目標：** 建立 Telegram bot 並連接 OpenClaw。

步驟：
1. 在 Telegram 搜尋 `@BotFather`
2. 發送 `/newbot`
3. 設定 bot 名稱與 username
4. 複製 bot token
5. 設定 OpenClaw Telegram gateway：
   ```
   openclaw gateway telegram --token <BOT_TOKEN>
   ```
6. 啟動 gateway：
   ```
   openclaw start
   ```

驗證：在 Telegram 對 bot 發訊息，確認收到回覆。

### Step 8：驗收

**目標：** 確認所有元件正常運作。

驗收清單：
- [ ] `openclaw --version` 顯示正確版本
- [ ] `openclaw config show` 顯示設定
- [ ] 從 Telegram 發訊息，agent 在 10 秒內回覆
- [ ] Agent 回覆內容合理（非錯誤訊息）

學完之後：
- 官方文件：[OpenClaw Docs]
- 社群：[Discord / GitHub Discussions]
- 更新指令：`npm update -g openclaw`

### Step 9：加碼

**目標：** 預覽進階功能，激發學員興趣。

展示內容：
- Skills 系統（讓 agent 學會新能力）
- 其他平台接通（Discord, WhatsApp, LINE）
- 多 agent 協作
- 自訂 system prompt
- 排程任務

不需要學員操作，僅展示 + 說明。

## 8. 已知風險點

| 風險 | 機率 | 影響 | 緩解措施 |
|------|------|------|----------|
| Node.js 安裝失敗（防毒阻擋） | 中 | 高 | 事先請學員暫停防毒、準備離線安裝包 |
| npm install 逾時（網路慢） | 中 | 中 | 預備離線 .tgz 安裝方式 |
| OpenRouter 註冊需信用卡 | 中 | 高 | 備案：用 Anthropic 免費試用額度 |
| Telegram bot token 複製錯誤 | 高 | 低 | 畫面放大、逐字確認 |
| openclaw init 互動式介面卡住 | 低 | 中 | 準備手動編輯設定檔的備案 |
| Windows Defender 阻擋 CLI | 中 | 中 | 加入例外清單的步驟 |
| API Key 額度不足 | 低 | 高 | 課前確認餘額、備用 Key |

## 9. 截圖規範

| 檔名 | 內容 | 步驟 |
|------|------|------|
| `step-1-winver.png` | winver 對話框 | 1 |
| `step-2-nvm-install.png` | nvm-windows 安裝畫面 | 2 |
| `step-2-node-version.png` | node --version 輸出 | 2 |
| `step-3-npm-install.png` | npm install -g openclaw 輸出 | 3 |
| `step-3-openclaw-version.png` | openclaw --version 輸出 | 3 |
| `step-4-openrouter-key.png` | OpenRouter API Key 頁面 | 4 |
| `step-5-openclaw-init.png` | openclaw init 互動畫面 | 5 |
| `step-6-first-chat.png` | 第一次對話畫面 | 6 |
| `step-7-botfather.png` | BotFather 建立 bot 畫面 | 7 |
| `step-7-telegram-reply.png` | Telegram bot 回覆畫面 | 7 |
| `step-8-health-check.png` | 驗收清單全部通過 | 8 |
