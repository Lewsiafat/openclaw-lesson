# openclaw-lesson

## 專案性質

純靜態 GitHub Pages 網站，零 build step。
雙擊 `index.html` 即可本地預覽（需要伺服器才能正常使用 localStorage）。

## 由來與走向

仿照 `hermes-windows-course` 的 wizard 架構，製作一堂 60 分鐘線上 1-on-1 課程，
教 Windows 使用者從零安裝 OpenClaw AI Agent 框架並完成第一次對話 + Telegram 接通。

OpenClaw 與 hermes-agent 的關鍵差異：
- OpenClaw 原生支援 Windows（透過 Node.js），不需要 WSL2
- 需要 Node.js >= 22.14
- 安裝方式：`npm install -g openclaw`
- 目標學員比 hermes 課程稍具技術背景

## 開發指令

```bash
# 本地預覽（任何 static server 皆可）
npx serve .
# 或
python3 -m http.server 8000
```

無需 npm install、無需 build。

## 架構重點

### Wizard 機制

- `wizard.js` 從 `<body data-total-steps="9" data-storage-key="openclaw-course-step">` 讀取參數
- 步驟以 `<section class="step" data-step="N">` 標記，用 `hidden` 屬性控制顯示
- URL hash (`#step-0` ~ `#step-9`) 可直接跳轉
- localStorage 記住進度
- `<pre data-copy>` 自動加上 Copy 按鈕

### 樣式

- Pico CSS（CDN）為基底
- `style.css` 只做微調（寬度上限、導覽列、copy 按鈕）

### 步驟結構

| Step | 標題 | 重點 |
|------|------|------|
| 0 | 前言 | 為什麼選 OpenClaw、與其他方案比較 |
| 1 | 確認前置需求 | Windows 11、管理員權限、網路 |
| 2 | 安裝 Node.js 22+ | nvm-windows 或直裝 |
| 3 | 安裝 OpenClaw CLI | `npm install -g openclaw` |
| 4 | 申請 API Key | OpenRouter / Anthropic / OpenAI |
| 5 | 初始化設定 | `openclaw init` / `openclaw setup` |
| 6 | 第一次對話 | 基本聊天測試 |
| 7 | 接通 Telegram | Gateway 設定 |
| 8 | 驗收 | Health check、後續方向 |
| 9 | 加碼 | Skills、進階功能預覽 |

## 內容編輯流程

1. 編輯 `index.html` 對應的 `<section class="step" data-step="N">`
2. 本地預覽確認排版
3. 若新增步驟，更新 `<body data-total-steps="N">`
4. 截圖放在 `screenshots/` 目錄（尚未建立）

## 兩份必讀的 Runbook

- **`pre-class-checklist.md`** — 上課前 10 分鐘跑一次，確認所有安裝指令還能用
- **`ai-runbook.md`** — AI 自動截圖 + 煙霧測試腳本

## 重要慣例

- 不做多語系（僅繁體中文）
- 不引入 build tooling（webpack / vite / etc.）
- 不加 framework（Vue / React / etc.）
- 所有 UI 文字用繁體中文，程式碼用英文
- 截圖檔名：`step-{N}-{描述}.png`

## Cross-step References

- Step 2 安裝的 Node.js 版本會影響 Step 3 的 npm 行為
- Step 4 取得的 API Key 在 Step 5 設定時使用
- Step 5 的設定檔路徑在 Step 7 接通 Telegram 時需要參照
- Step 6 的成功對話是 Step 8 驗收的前提
