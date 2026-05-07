# AI Runbook — OpenClaw Windows 安裝課程

本文件供 AI agent 自動執行截圖與煙霧測試使用。

---

## Part 1: Full Capture Run（完整截圖流程）

### 環境需求
- Windows 11 虛擬機或實機
- 螢幕解析度 1920x1080
- 截圖寬度統一 800px
- 輸出目錄：`screenshots/`

### 截圖清單

| 序號 | 操作 | 截圖檔名 | 說明 |
|------|------|----------|------|
| 1 | 開啟「執行」輸入 `winver` | `step-1-winver.png` | Windows 版本對話框 |
| 2 | 開啟 nvm-windows installer | `step-2-nvm-install.png` | 安裝精靈畫面 |
| 3 | 執行 `node --version` | `step-2-node-version.png` | 版本號輸出 |
| 4 | 執行 `npm install -g openclaw` | `step-3-npm-install.png` | 安裝過程輸出 |
| 5 | 執行 `openclaw --version` | `step-3-openclaw-version.png` | 版本號輸出 |
| 6 | OpenRouter API Key 頁面 | `step-4-openrouter-key.png` | Key 建立成功畫面（遮蔽 Key） |
| 7 | 執行 `openclaw init` | `step-5-openclaw-init.png` | 互動式設定畫面 |
| 8 | 執行 `openclaw chat` | `step-6-first-chat.png` | 第一次對話畫面 |
| 9 | BotFather `/newbot` 流程 | `step-7-botfather.png` | Bot 建立成功訊息 |
| 10 | Telegram bot 回覆 | `step-7-telegram-reply.png` | Bot 成功回覆使用者訊息 |
| 11 | 驗收完成 | `step-8-health-check.png` | 所有檢查通過 |

### 截圖流程

```
對每個截圖項目：
1. 執行對應操作
2. 等待結果出現
3. 截圖（800px 寬）
4. 儲存至 screenshots/ 目錄
5. 確認檔名正確
```

### 注意事項
- API Key 截圖必須遮蔽實際 Key 值
- 終端機截圖確保字體清晰可讀
- 如遇錯誤，先截圖錯誤畫面再排除

---

## Part 2: Quick Smoke Test（快速煙霧測試）

上課前快速驗證，不截圖，僅確認指令可用。

### 測試步驟

```bash
# 1. Node.js
node --version
# 預期：v22.x.x

# 2. npm
npm --version
# 預期：10.x.x

# 3. OpenClaw CLI
openclaw --version
# 預期：有版本號輸出

# 4. OpenClaw init（確認互動式介面啟動）
# 手動執行，確認畫面正常後 Ctrl+C
openclaw init

# 5. 網路連線
curl -s https://openrouter.ai/ | head -1
# 預期：有 HTML 輸出
```

### 判定標準

- 全部通過 → 可以上課
- 1-2 項失敗 → 準備備案，仍可上課
- 3 項以上失敗 → 延期，排除問題後重測
