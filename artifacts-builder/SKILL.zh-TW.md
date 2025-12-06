---
name: artifacts-builder
description: 用於建立精緻、多組件 claude.ai HTML artifacts 的工具套件，使用現代前端網頁技術（React、Tailwind CSS、shadcn/ui）。適用於需要狀態管理、路由或 shadcn/ui 元件的複雜 artifacts - 不適用於簡單的單檔案 HTML/JSX artifacts。
license: 完整條款請參閱 LICENSE.txt
---

# Artifacts Builder

要建立強大的前端 claude.ai artifacts，請遵循以下步驟：
1. 使用 `scripts/init-artifact.sh` 初始化前端儲存庫
2. 透過編輯生成的程式碼來開發您的 artifact
3. 使用 `scripts/bundle-artifact.sh` 將所有程式碼打包成單一 HTML 檔案
4. 向使用者展示 artifact
5. （可選）測試 artifact

**技術堆疊**：React 18 + TypeScript + Vite + Parcel（打包）+ Tailwind CSS + shadcn/ui

## 設計與風格指南

非常重要：為了避免通常被稱為「AI 俗套」的情況，請避免使用過多的置中佈局、紫色漸層、統一的圓角和 Inter 字體。

## 快速開始

### 步驟 1：初始化專案

執行初始化腳本以建立新的 React 專案：
```bash
bash scripts/init-artifact.sh <project-name>
cd <project-name>
```

這將建立一個完全設定的專案，包括：
- ✅ React + TypeScript（透過 Vite）
- ✅ Tailwind CSS 3.4.1 與 shadcn/ui 主題系統
- ✅ 路徑別名（`@/`）已設定
- ✅ 預先安裝 40+ shadcn/ui 元件
- ✅ 包含所有 Radix UI 相依性
- ✅ 已設定 Parcel 用於打包（透過 .parcelrc）
- ✅ Node 18+ 相容性（自動偵測並固定 Vite 版本）

### 步驟 2：開發您的 Artifact

要建立 artifact，請編輯生成的檔案。請參閱下方的**常見開發任務**以獲取指導。

### 步驟 3：打包成單一 HTML 檔案

要將 React 應用程式打包成單一 HTML artifact：
```bash
bash scripts/bundle-artifact.sh
```

這將建立 `bundle.html` - 一個獨立的 artifact，內嵌所有 JavaScript、CSS 和相依性。此檔案可以直接在 Claude 對話中作為 artifact 分享。

**要求**：您的專案必須在根目錄中有 `index.html`。

**腳本功能**：
- 安裝打包相依性（parcel、@parcel/config-default、parcel-resolver-tspaths、html-inline）
- 建立支援路徑別名的 `.parcelrc` 設定
- 使用 Parcel 建置（無 source maps）
- 使用 html-inline 將所有資源內嵌到單一 HTML 中

### 步驟 4：與使用者分享 Artifact

最後，在對話中與使用者分享打包的 HTML 檔案，以便他們可以將其視為 artifact 查看。

### 步驟 5：測試/視覺化 Artifact（可選）

注意：這是完全可選的步驟。僅在必要或被要求時執行。

要測試/視覺化 artifact，請使用可用的工具（包括其他 Skills 或內建工具，如 Playwright 或 Puppeteer）。一般來說，避免預先測試 artifact，因為這會在請求和完成的 artifact 可見之間增加延遲。如果被要求或出現問題，請在展示 artifact 後再進行測試。

## 參考資料

- **shadcn/ui 元件**：https://ui.shadcn.com/docs/components
