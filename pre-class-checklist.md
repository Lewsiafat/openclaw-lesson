# 課前驗證清單

上課前 10 分鐘跑一次，確保所有安裝指令與流程仍然可用。

---

## 1. Node.js 安裝來源

- [ ] nvm-windows releases 頁面可存取：https://github.com/coreybutler/nvm-windows/releases
- [ ] Node.js 官網可存取：https://nodejs.org/
- [ ] 確認目前 LTS 版本號 >= 22.14

```
# 若本機有 node，確認版本
node --version
```

預期：`v22.x.x` 以上

## 2. OpenClaw CLI 安裝

- [ ] `npm install -g openclaw` 可正常完成（無錯誤）
- [ ] `openclaw --version` 有輸出

```
npm install -g openclaw
openclaw --version
```

若失敗：檢查 npm registry 是否可連、是否有權限問題。

## 3. API Key 申請流程

- [ ] OpenRouter 註冊頁面可存取：https://openrouter.ai/
- [ ] API Key 建立流程無變動（settings → keys → create）
- [ ] 備案：Anthropic Console 可存取：https://console.anthropic.com/

## 4. Telegram Bot 建立

- [ ] @BotFather 可正常回應 `/newbot`
- [ ] Bot token 格式正確（數字:字串）

## 5. 課程頁面

- [ ] GitHub Pages 可存取：https://lewsiafat.github.io/openclaw-lesson/
- [ ] 所有步驟可正常切換（Step 0-9）
- [ ] 指令可複製（Copy 按鈕正常）

---

## 如果有項目失敗

1. 記下失敗原因
2. 準備替代方案（離線安裝包、備用 API Key 等）
3. 在課程開頭先告知學員調整
