---
name: docx
description: "全方位的文件建立、編輯和分析功能，支援追蹤修訂、註解、格式保留和文字擷取。當 Claude 需要處理專業文件（.docx 檔案）時使用，包括：(1) 建立新文件、(2) 修改或編輯內容、(3) 處理追蹤修訂、(4) 新增註解，或任何其他文件相關任務"
license: Proprietary. LICENSE.txt has complete terms
---

# DOCX 建立、編輯和分析

## 概述

使用者可能會要求您建立、編輯或分析 .docx 檔案的內容。.docx 檔案本質上是一個包含 XML 檔案和其他資源的 ZIP 壓縮檔，您可以讀取或編輯這些內容。針對不同的任務，您有不同的工具和工作流程可供使用。

## 工作流程決策樹

### 讀取/分析內容
使用下方的「文字擷取」或「原始 XML 存取」章節

### 建立新文件
使用「建立新 Word 文件」工作流程

### 編輯現有文件
- **您自己的文件 + 簡單修改**
  使用「基本 OOXML 編輯」工作流程

- **他人的文件**
  使用**「紅線修訂工作流程」**（建議預設方式）

- **法律、學術、商業或政府文件**
  使用**「紅線修訂工作流程」**（必要）

## 讀取和分析內容

### 文字擷取
如果您只需要讀取文件的文字內容，應該使用 pandoc 將文件轉換為 markdown 格式。Pandoc 提供優秀的文件結構保留支援，並可顯示追蹤修訂：

```bash
# 將文件轉換為包含追蹤修訂的 markdown
pandoc --track-changes=all path-to-file.docx -o output.md
# 選項：--track-changes=accept/reject/all
```

### 原始 XML 存取
您需要原始 XML 存取來處理：註解、複雜格式、文件結構、嵌入媒體和中繼資料。若要使用這些功能，您需要解壓縮文件並讀取其原始 XML 內容。

#### 解壓縮檔案
`python ooxml/scripts/unpack.py <office_file> <output_directory>`

#### 主要檔案結構
* `word/document.xml` - 主要文件內容
* `word/comments.xml` - document.xml 中參照的註解
* `word/media/` - 嵌入的圖片和媒體檔案
* 追蹤修訂使用 `<w:ins>`（插入）和 `<w:del>`（刪除）標籤

## 建立新 Word 文件

從頭建立新 Word 文件時，請使用 **docx-js**，它允許您使用 JavaScript/TypeScript 建立 Word 文件。

### 工作流程
1. **必要 - 讀取完整檔案**：完整從頭到尾讀取 [`docx-js.md`](docx-js.md)（約 500 行）。**絕對不要在讀取此檔案時設定任何範圍限制。** 在進行文件建立之前，請先閱讀完整檔案內容，了解詳細語法、重要格式規則和最佳實踐。
2. 使用 Document、Paragraph、TextRun 元件建立 JavaScript/TypeScript 檔案（您可以假設所有相依套件都已安裝，但如果沒有，請參考下方的相依套件章節）
3. 使用 Packer.toBuffer() 匯出為 .docx 檔案

## 編輯現有 Word 文件

編輯現有 Word 文件時，請使用 **Document 函式庫**（一個用於 OOXML 操作的 Python 函式庫）。此函式庫會自動處理基礎架構設定，並提供文件操作方法。對於複雜情境，您可以透過函式庫直接存取底層 DOM。

### 工作流程
1. **必要 - 讀取完整檔案**：完整從頭到尾讀取 [`ooxml.md`](ooxml.md)（約 600 行）。**絕對不要在讀取此檔案時設定任何範圍限制。** 閱讀完整檔案內容以了解 Document 函式庫 API 和直接編輯文件檔案的 XML 模式。
2. 解壓縮文件：`python ooxml/scripts/unpack.py <office_file> <output_directory>`
3. 使用 Document 函式庫建立並執行 Python 腳本（請參考 ooxml.md 中的「Document Library」章節）
4. 打包最終文件：`python ooxml/scripts/pack.py <input_directory> <office_file>`

Document 函式庫提供常見操作的高階方法，以及複雜情境的直接 DOM 存取。

## 文件審閱的紅線修訂工作流程

此工作流程允許您在 OOXML 中實作之前，使用 markdown 規劃全面的追蹤修訂。**重要**：對於完整的追蹤修訂，您必須系統性地實作所有變更。

**批次處理策略**：將相關變更分組為 3-10 個變更的批次。這樣可以讓除錯變得易於管理，同時維持效率。在移至下一批次之前，先測試每個批次。

**原則：最小化、精確的編輯**
實作追蹤修訂時，只標記實際變更的文字。重複未變更的文字會讓編輯更難審閱，且顯得不專業。將替換分解為：[未變更文字] + [刪除] + [插入] + [未變更文字]。透過從原始元素中擷取 `<w:r>` 元素並重新使用，來保留原始執行的 RSID（對於未變更的文字）。

範例 - 將句子中的「30 days」改為「60 days」：
```python
# 不良 - 替換整個句子
'<w:del><w:r><w:delText>The term is 30 days.</w:delText></w:r></w:del><w:ins><w:r><w:t>The term is 60 days.</w:t></w:r></w:ins>'

# 良好 - 只標記變更的部分，保留未變更文字的原始 <w:r>
'<w:r w:rsidR="00AB12CD"><w:t>The term is </w:t></w:r><w:del><w:r><w:delText>30</w:delText></w:r></w:del><w:ins><w:r><w:t>60</w:t></w:r></w:ins><w:r w:rsidR="00AB12CD"><w:t> days.</w:t></w:r>'
```

### 追蹤修訂工作流程

1. **取得 markdown 表示**：將文件轉換為保留追蹤修訂的 markdown：
   ```bash
   pandoc --track-changes=all path-to-file.docx -o current.md
   ```

2. **識別並分組變更**：審閱文件並識別所有需要的變更，將它們組織成邏輯批次：

   **定位方法**（用於在 XML 中尋找變更）：
   - 章節/標題編號（例如：「第 3.2 節」、「第四條」）
   - 段落識別碼（如有編號）
   - 使用獨特周圍文字的 Grep 模式
   - 文件結構（例如：「第一段」、「簽名區塊」）
   - **不要使用 markdown 行號** - 它們無法對應到 XML 結構

   **批次組織**（每批次分組 3-10 個相關變更）：
   - 按章節：「批次 1：第 2 節修訂」、「批次 2：第 5 節更新」
   - 按類型：「批次 1：日期更正」、「批次 2：當事人名稱變更」
   - 按複雜度：從簡單的文字替換開始，然後處理複雜的結構變更
   - 循序：「批次 1：第 1-3 頁」、「批次 2：第 4-6 頁」

3. **讀取文件並解壓縮**：
   - **必要 - 讀取完整檔案**：完整從頭到尾讀取 [`ooxml.md`](ooxml.md)（約 600 行）。**絕對不要在讀取此檔案時設定任何範圍限制。** 特別注意「Document Library」和「Tracked Change Patterns」章節。
   - **解壓縮文件**：`python ooxml/scripts/unpack.py <file.docx> <dir>`
   - **記下建議的 RSID**：解壓縮腳本會建議一個用於追蹤修訂的 RSID。複製此 RSID 以在步驟 4b 中使用。

4. **批次實作變更**：按邏輯分組變更（按章節、類型或接近度），並在單一腳本中一起實作它們。此方法：
   - 讓除錯更容易（較小的批次 = 更容易隔離錯誤）
   - 允許漸進式進展
   - 維持效率（3-10 個變更的批次大小效果良好）

   **建議的批次分組：**
   - 按文件章節（例如：「第 3 節變更」、「定義」、「終止條款」）
   - 按變更類型（例如：「日期變更」、「當事人名稱更新」、「法律術語替換」）
   - 按接近度（例如：「第 1-3 頁的變更」、「文件前半部的變更」）

   對於每批相關變更：

   **a. 將文字對應到 XML**：在 `word/document.xml` 中 Grep 文字，以驗證文字如何分割在 `<w:r>` 元素中。

   **b. 建立並執行腳本**：使用 `get_node` 尋找節點，實作變更，然後 `doc.save()`。請參考 ooxml.md 中的 **「Document Library」** 章節以了解模式。

   **注意**：在撰寫腳本之前，務必立即 grep `word/document.xml` 以取得當前行號並驗證文字內容。行號會在每次腳本執行後變更。

5. **打包文件**：完成所有批次後，將解壓縮的目錄轉換回 .docx：
   ```bash
   python ooxml/scripts/pack.py unpacked reviewed-document.docx
   ```

6. **最終驗證**：對完整文件進行全面檢查：
   - 將最終文件轉換為 markdown：
     ```bash
     pandoc --track-changes=all reviewed-document.docx -o verification.md
     ```
   - 驗證所有變更都已正確套用：
     ```bash
     grep "original phrase" verification.md  # 應該找不到
     grep "replacement phrase" verification.md  # 應該找得到
     ```
   - 檢查沒有引入非預期的變更


## 將文件轉換為圖片

若要視覺化分析 Word 文件，請使用兩步驟流程將其轉換為圖片：

1. **將 DOCX 轉換為 PDF**：
   ```bash
   soffice --headless --convert-to pdf document.docx
   ```

2. **將 PDF 頁面轉換為 JPEG 圖片**：
   ```bash
   pdftoppm -jpeg -r 150 document.pdf page
   ```
   這會建立 `page-1.jpg`、`page-2.jpg` 等檔案。

選項：
- `-r 150`：設定解析度為 150 DPI（調整以平衡品質/大小）
- `-jpeg`：輸出 JPEG 格式（如果偏好 PNG，使用 `-png`）
- `-f N`：要轉換的第一頁（例如：`-f 2` 從第 2 頁開始）
- `-l N`：要轉換的最後一頁（例如：`-l 5` 在第 5 頁停止）
- `page`：輸出檔案的前綴

特定範圍範例：
```bash
pdftoppm -jpeg -r 150 -f 2 -l 5 document.pdf page  # 僅轉換第 2-5 頁
```

## 程式碼風格指南
**重要**：為 DOCX 操作產生程式碼時：
- 撰寫簡潔的程式碼
- 避免冗長的變數名稱和重複的操作
- 避免不必要的 print 陳述式

## 相依套件

必要的相依套件（如果未安裝，請安裝）：

- **pandoc**：`sudo apt-get install pandoc`（用於文字擷取）
- **docx**：`npm install -g docx`（用於建立新文件）
- **LibreOffice**：`sudo apt-get install libreoffice`（用於 PDF 轉換）
- **Poppler**：`sudo apt-get install poppler-utils`（用於 pdftoppm 將 PDF 轉換為圖片）
- **defusedxml**：`pip install defusedxml`（用於安全的 XML 解析）