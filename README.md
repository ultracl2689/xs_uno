# xs_uno

UNO 大賽 x XS 能量飲料活動網站，使用 Vue 3 + Vite + Element Plus + Tailwind CSS 建立，部署於 GitHub Pages。

## 開發

```bash
bun install
bun dev          # 啟動開發伺服器
bun run build    # 建置 production 版本到 dist/
bun preview      # 本地預覽 production 建置
```

## 部署到 GitHub Pages

本專案透過 **GitHub Actions 自動部署**，不需要手動 build 或 commit `dist/`。

### 運作方式

每次 push 到 `main` 分支時，`.github/workflows/deploy.yml` 會自動：

1. 安裝相依套件（`bun install --frozen-lockfile`）
2. 執行建置（`bun run build`），產出在 `dist/`
3. 將 `dist/` 上傳並部署到 GitHub Pages

部署完成後網站位於：`https://<帳號>.github.io/xs_uno/`

### 首次設定（只需做一次）

1. 確認 `vite.config.js` 的 `base` 與 repo 名稱一致：

   ```js
   export default defineConfig({
     base: '/xs_uno/',
     // ...
   })
   ```

   > base path 必須正確，否則部署後 JS／CSS／圖片路徑會錯誤，導致**白畫面**。

2. 到 GitHub repo 的 **Settings → Pages → Build and deployment → Source**，
   選擇 **GitHub Actions**（不是 "Deploy from a branch"）。

3. push 到 `main` 即會自動部署：

   ```bash
   git add .
   git commit -m "your message"
   git push origin main
   ```

   可在 repo 的 **Actions** 分頁查看部署進度。

### 注意事項

- `dist/` 與 `node_modules/` 已列入 `.gitignore`，**不要**手動 commit 建置產物——一律由 CI 建置，避免推到舊版或其他專案的產物造成畫面異常。
- 根目錄的 `index.html` 是 Vite 開發入口（引用 `/src/main.js`），僅供本地開發使用，不可直接拿來當作 Pages 的部署檔。
