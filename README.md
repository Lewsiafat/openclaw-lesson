# openclaw-lesson

60 分鐘互動課程，帶 Windows 使用者從零安裝並上手 OpenClaw AI Agent 框架。

**Live:** <https://lewsiafat.github.io/openclaw-lesson/>

---

## 結構

```
index.html          ← 單頁 wizard（Step 0 前言 + Steps 1-9）
wizard.js           ← 通用步驟切換邏輯（與 hermes-windows-course 共用）
style.css           ← Pico CSS 補充樣式
pre-class-checklist.md  ← 上課前快速驗證清單
ai-runbook.md       ← AI 截圖 / 煙霧測試腳本
docs/superpowers/
  specs/            ← 課程設計規格書
  plans/            ← 實作計畫
```

## 上次驗證

| 項目 | 日期 | 結果 |
|------|------|------|
| Node.js 安裝指令 | — | — |
| OpenClaw CLI 安裝 | — | — |
| Telegram 接通 | — | — |

## 更新內容

- 2026-05-07：建立專案骨架、課程設計規格書、實作計畫

## 部署

GitHub Pages 從 `main` branch 根目錄直接 serve。

1. Push 到 `main`
2. GitHub Pages 自動部署
3. 無需 build step

## License

MIT
