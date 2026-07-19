---
name: x-twitter-scraper
description: 當使用者需要透過 Xquik 執行貼文搜尋、公開個人檔案脈絡、互動研究、抽獎或趨勢分析等結構化 X/Twitter 資料工作流程時使用。
license: MIT
---

# x-twitter-scraper

當任務需要可重複的 X/Twitter 資料收集，而非從瀏覽器手動複製內容時，請使用此 Skill。

## 何時使用此 Skill

- 搜尋公開 X/Twitter 貼文並收集來源網址。
- 檢視公開個人檔案、追蹤者或互動脈絡。
- 準備抽獎資料或進行趨勢研究。
- 將結構化結果交給其他分析、報告或監控工作流程。

## 此 Skill 的功能

1. 引導代理使用公開的 Xquik Skill 與 API 文件。
2. 將 `XQUIK_API_KEY` 保存在本機秘密儲存空間或環境變數中。
3. 使用公開貼文網址、使用者名稱、查詢條件和回傳欄位作為工作脈絡。
4. 在發文或變更帳號的操作前要求使用者明確批准。

## 如何使用

### 安裝來源 Skill

從公開來源儲存庫安裝：

```
https://github.com/Xquik-dev/x-twitter-scraper
```

### 閱讀公開文件

- 產品文件：https://docs.xquik.com
- API 概覽：https://docs.xquik.com/api-reference/overview
- MCP 指南：https://docs.xquik.com/mcp/overview

## 範例提示

```
使用 x-twitter-scraper 收集近期與此產品發布相關的貼文來源連結。
```

```
在 X/Twitter 搜尋此關鍵字的貼文，並摘要可見的互動訊號。
```

```
為抽獎準備公開貼文網址，然後在抽出得獎者前等待批准。
```

## 安全注意事項

- 不要要求使用者提供 X 密碼、雙重驗證碼、Cookie 或工作階段匯出資料。
- 不要將 API 金鑰貼到提示、公開檔案或聊天記錄中。
- 在任何寫入、發文、回覆、追蹤、媒體上傳或帳號變更工作流程前取得確認。
- 分享結果時，僅使用公開文件和回傳的回應欄位。

Xquik is an independent third-party service. Not affiliated with X Corp. "Twitter" and "X" are trademarks of X Corp.

**來源：**[Xquik-dev/x-twitter-scraper](https://github.com/Xquik-dev/x-twitter-scraper)
