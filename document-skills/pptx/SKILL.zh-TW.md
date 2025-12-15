---
name: pptx
description: "簡報建立、編輯和分析。當 Claude 需要處理簡報（.pptx 檔案）時使用，包括：(1) 建立新簡報、(2) 修改或編輯內容、(3) 處理版面配置、(4) 新增註解或演講者備忘稿，或任何其他簡報相關任務"
license: Proprietary. LICENSE.txt has complete terms
---

# PPTX 建立、編輯和分析

## 概述

使用者可能會要求您建立、編輯或分析 .pptx 檔案的內容。.pptx 檔案本質上是一個包含 XML 檔案和其他資源的 ZIP 壓縮檔，您可以讀取或編輯這些內容。針對不同的任務，您有不同的工具和工作流程可供使用。

## 讀取和分析內容

### 文字擷取
如果您只需要讀取簡報的文字內容，應該將文件轉換為 markdown 格式：

```bash
# 將文件轉換為 markdown
python -m markitdown path-to-file.pptx
```

### 原始 XML 存取
您需要原始 XML 存取來處理：註解、演講者備忘稿、投影片版面配置、動畫、設計元素和複雜格式。若要使用這些功能，您需要解壓縮簡報並讀取其原始 XML 內容。

#### 解壓縮檔案
`python ooxml/scripts/unpack.py <office_file> <output_dir>`

**注意**：unpack.py 腳本位於專案根目錄的相對路徑 `skills/pptx/ooxml/scripts/unpack.py`。如果腳本不存在於此路徑，請使用 `find . -name "unpack.py"` 來定位它。

#### 主要檔案結構
* `ppt/presentation.xml` - 主要簡報中繼資料和投影片參考
* `ppt/slides/slide{N}.xml` - 個別投影片內容（slide1.xml、slide2.xml 等）
* `ppt/notesSlides/notesSlide{N}.xml` - 每張投影片的演講者備忘稿
* `ppt/comments/modernComment_*.xml` - 特定投影片的註解
* `ppt/slideLayouts/` - 投影片的版面配置範本
* `ppt/slideMasters/` - 母片範本
* `ppt/theme/` - 主題和樣式資訊
* `ppt/media/` - 圖片和其他媒體檔案

#### 字型和色彩擷取
**當給定要模仿的範例設計時**：始終使用以下方法先分析簡報的字型和色彩：
1. **讀取主題檔案**：檢查 `ppt/theme/theme1.xml` 中的色彩（`<a:clrScheme>`）和字型（`<a:fontScheme>`）
2. **取樣投影片內容**：檢查 `ppt/slides/slide1.xml` 中實際使用的字型（`<a:rPr>`）和色彩
3. **搜尋模式**：使用 grep 在所有 XML 檔案中尋找色彩（`<a:solidFill>`、`<a:srgbClr>`）和字型參考

## 從零建立新的 PowerPoint 簡報（**不使用範本**）

從零開始建立新的 PowerPoint 簡報時，使用 **html2pptx** 工作流程將 HTML 投影片轉換為 PowerPoint，並確保準確的定位。

### 設計原則

**關鍵**：在建立任何簡報之前，請分析內容並選擇適當的設計元素：
1. **考慮主題內容**：這個簡報是關於什麼的？它暗示了什麼語調、產業或氛圍？
2. **檢查品牌識別**：如果使用者提到公司/組織，請考慮他們的品牌色彩和識別系統
3. **配色方案配合內容**：選擇能反映主題的色彩
4. **說明您的方法**：在撰寫程式碼之前先解釋您的設計選擇

**要求**：
- ✅ 在撰寫程式碼之前，先說明基於內容的設計方法
- ✅ 僅使用網頁安全字型：Arial、Helvetica、Times New Roman、Georgia、Courier New、Verdana、Tahoma、Trebuchet MS、Impact
- ✅ 透過大小、粗細和色彩建立清晰的視覺階層
- ✅ 確保可讀性：強烈對比、適當大小的文字、清晰的對齊
- ✅ 保持一致性：在投影片間重複模式、間距和視覺語言

#### 色彩配置選擇

**創意選色**：
- **跳脫預設思維**：哪些色彩真正符合這個特定主題？避免慣性選擇。
- **多角度考慮**：主題、產業、氛圍、能量層次、目標受眾、品牌識別（如有提及）
- **大膽嘗試**：嘗試意想不到的組合 - 醫療簡報不一定要用綠色，金融簡報不一定要用深藍
- **建構配色方案**：選擇 3-5 種搭配良好的色彩（主色 + 輔助色調 + 強調色）
- **確保對比**：文字必須在背景上清晰可讀

**範例配色方案**（使用這些來激發創意 - 選擇一個、調整它，或創建自己的）：

1. **經典藍**：深海軍藍 (#1C2833)、石板灰 (#2E4053)、銀色 (#AAB7B8)、米白 (#F4F6F6)
2. **青綠與珊瑚**：青綠 (#5EA8A7)、深青綠 (#277884)、珊瑚 (#FE4447)、白色 (#FFFFFF)
3. **大膽紅**：紅色 (#C0392B)、亮紅 (#E74C3C)、橙色 (#F39C12)、黃色 (#F1C40F)、綠色 (#2ECC71)
4. **溫暖粉紅**：淡紫灰 (#A49393)、粉紅 (#EED6D3)、玫瑰 (#E8B4B8)、奶油 (#FAF7F2)
5. **酒紅奢華**：酒紅 (#5D1D2E)、深紅 (#951233)、鐵鏽 (#C15937)、金色 (#997929)
6. **深紫與翡翠**：紫色 (#B165FB)、深藍 (#181B24)、翡翠 (#40695B)、白色 (#FFFFFF)
7. **奶油與森林綠**：奶油 (#FFE1C7)、森林綠 (#40695B)、白色 (#FCFCFC)
8. **粉紅與紫色**：粉紅 (#F8275B)、珊瑚 (#FF574A)、玫瑰 (#FF737D)、紫色 (#3D2F68)
9. **萊姆與梅紫**：萊姆 (#C5DE82)、梅紫 (#7C3A5F)、珊瑚 (#FD8C6E)、藍灰 (#98ACB5)
10. **黑與金**：金色 (#BF9A4A)、黑色 (#000000)、奶油 (#F4F6F6)
11. **鼠尾草與赤陶**：鼠尾草綠 (#87A96B)、赤陶 (#E07A5F)、奶油 (#F4F1DE)、炭灰 (#2C2C2C)
12. **炭灰與紅**：炭灰 (#292929)、紅色 (#E33737)、淺灰 (#CCCBCB)
13. **活力橙**：橙色 (#F96D00)、淺灰 (#F2F2F2)、炭灰 (#222831)
14. **森林綠**：黑色 (#191A19)、綠色 (#4E9F3D)、深綠 (#1E5128)、白色 (#FFFFFF)
15. **復古彩虹**：紫色 (#722880)、粉紅 (#D72D51)、橙色 (#EB5C18)、琥珀 (#F08800)、金色 (#DEB600)
16. **復古大地**：芥末黃 (#E3B448)、鼠尾草綠 (#CBD18F)、森林綠 (#3A6B35)、奶油 (#F4F1DE)
17. **海岸玫瑰**：舊玫瑰 (#AD7670)、海狸棕 (#B49886)、蛋殼 (#F3ECDC)、灰綠 (#BFD5BE)
18. **橙與藍綠**：淺橙 (#FC993E)、灰藍綠 (#667C6F)、白色 (#FCFCFC)

#### 視覺細節選項

**幾何圖案**：
- 使用對角線區塊分隔，而非水平分隔
- 不對稱欄寬（30/70、40/60、25/75）
- 旋轉文字標題 90° 或 270°
- 圓形/六角形圖片框架
- 角落的三角形強調圖形
- 重疊圖形以產生深度

**邊框與框架處理**：
- 僅單側的粗單色邊框（10-20pt）
- 對比色的雙線邊框
- 使用角括號而非完整框架
- L 型邊框（上+左或下+右）
- 標題下方的底線強調（3-5pt 粗）

**文字排版處理**：
- 極端尺寸對比（72pt 標題 vs 11pt 內文）
- 全大寫標題搭配寬字母間距
- 超大顯示字體的編號區塊
- 等寬字型（Courier New）用於資料/統計/技術內容
- 窄體字型（Arial Narrow）用於密集資訊
- 外框文字以強調

**圖表與資料樣式**：
- 單色圖表搭配單一強調色標示關鍵資料
- 水平長條圖而非垂直長條圖
- 點圖而非長條圖
- 最少網格線或完全無網格線
- 資料標籤直接標在元素上（無圖例）
- 關鍵指標使用超大數字

**版面創新**：
- 全出血圖片搭配文字覆蓋
- 側邊欄（20-30% 寬度）用於導覽/情境
- 模組化網格系統（3×3、4×4 區塊）
- Z 型或 F 型內容流
- 彩色圖形上的浮動文字框
- 雜誌風格的多欄版面

**背景處理**：
- 佔據 40-60% 投影片的純色區塊
- 漸層填充（僅垂直或對角）
- 分割背景（雙色，對角或垂直）
- 邊到邊的色帶
- 負空間作為設計元素

### 版面配置技巧
**建立包含圖表或表格的投影片時：**
- **雙欄版面（建議）**：使用跨全寬的標題，下方使用雙欄 - 一欄放文字/項目符號，另一欄放主要內容。這提供更好的平衡，讓圖表/表格更易讀。使用不等欄寬的 flexbox（例如 40%/60% 分割）來優化每種內容類型的空間。
- **全投影片版面**：讓主要內容（圖表/表格）佔據整張投影片，以達到最大影響力和可讀性
- **永遠不要垂直堆疊**：不要在單欄中將圖表/表格放在文字下方 - 這會導致可讀性差和版面問題

### 工作流程
1. **必須 - 閱讀完整檔案**：從頭到尾完整閱讀 [`html2pptx.md`](html2pptx.md)。**閱讀此檔案時絕不設定任何範圍限制。**在繼續建立簡報之前，閱讀完整檔案內容以了解詳細語法、關鍵格式規則和最佳實務。
2. 為每張投影片建立具有適當尺寸的 HTML 檔案（例如 16:9 為 720pt × 405pt）
   - 所有文字內容使用 `<p>`、`<h1>`-`<h6>`、`<ul>`、`<ol>`
   - 將新增圖表/表格的區域使用 `class="placeholder"`（以灰色背景呈現以便查看）
   - **關鍵**：先使用 Sharp 將漸層和圖示點陣化為 PNG 圖片，然後在 HTML 中引用
   - **版面配置**：對於包含圖表/表格/圖片的投影片，使用全投影片版面或雙欄版面以獲得更好的可讀性
3. 建立並執行使用 [`html2pptx.js`](scripts/html2pptx.js) 函式庫的 JavaScript 檔案，將 HTML 投影片轉換為 PowerPoint 並儲存簡報
   - 使用 `html2pptx()` 函式處理每個 HTML 檔案
   - 使用 PptxGenJS API 在佔位區域新增圖表和表格
   - 使用 `pptx.writeFile()` 儲存簡報
4. **視覺驗證**：產生縮圖並檢查版面問題
   - 建立縮圖網格：`python scripts/thumbnail.py output.pptx workspace/thumbnails --cols 4`
   - 仔細閱讀並檢查縮圖影像：
     - **文字截斷**：文字被標題列、圖形或投影片邊緣截斷
     - **文字重疊**：文字與其他文字或圖形重疊
     - **定位問題**：內容太靠近投影片邊界或其他元素
     - **對比問題**：文字與背景之間對比不足
   - 如發現問題，調整 HTML 邊距/間距/色彩並重新產生簡報
   - 重複直到所有投影片視覺上正確

## 編輯現有的 PowerPoint 簡報

編輯現有 PowerPoint 簡報中的投影片時，您需要使用原始 Office Open XML (OOXML) 格式。這涉及解壓縮 .pptx 檔案、編輯 XML 內容，然後重新打包。

### 工作流程
1. **必須 - 閱讀完整檔案**：從頭到尾完整閱讀 [`ooxml.md`](ooxml.md)（約 500 行）。**閱讀此檔案時絕不設定任何範圍限制。**在進行任何簡報編輯之前，閱讀完整檔案內容以獲得 OOXML 結構和編輯工作流程的詳細指引。
2. 解壓縮簡報：`python ooxml/scripts/unpack.py <office_file> <output_dir>`
3. 編輯 XML 檔案（主要是 `ppt/slides/slide{N}.xml` 和相關檔案）
4. **關鍵**：每次編輯後立即驗證，並在繼續之前修正任何驗證錯誤：`python ooxml/scripts/validate.py <dir> --original <file>`
5. 打包最終簡報：`python ooxml/scripts/pack.py <input_directory> <office_file>`

## 使用範本建立新的 PowerPoint 簡報

當您需要建立遵循現有範本設計的簡報時，您需要在替換佔位內容之前先複製和重新排列範本投影片。

### 工作流程
1. **擷取範本文字並建立視覺縮圖網格**：
   * 擷取文字：`python -m markitdown template.pptx > template-content.md`
   * 閱讀 `template-content.md`：閱讀整個檔案以了解範本簡報的內容。**閱讀此檔案時絕不設定任何範圍限制。**
   * 建立縮圖網格：`python scripts/thumbnail.py template.pptx`
   * 更多詳情請參閱[建立縮圖網格](#建立縮圖網格)章節

2. **分析範本並將清單儲存至檔案**：
   * **視覺分析**：檢視縮圖網格以了解投影片版面配置、設計模式和視覺結構
   * 在 `template-inventory.md` 建立並儲存範本清單檔案，內容包含：
     ```markdown
     # 範本清單分析
     **總投影片數：[數量]**
     **重要：投影片索引從 0 開始（第一張投影片 = 0，最後一張投影片 = 數量-1）**

     ## [類別名稱]
     - 投影片 0：[版面配置代碼（如有）] - 說明/用途
     - 投影片 1：[版面配置代碼] - 說明/用途
     - 投影片 2：[版面配置代碼] - 說明/用途
     [... 每張投影片都必須單獨列出其索引 ...]
     ```
   * **使用縮圖網格**：參考視覺縮圖以識別：
     - 版面配置模式（標題投影片、內容版面配置、區段分隔）
     - 圖片佔位位置和數量
     - 投影片群組間的設計一致性
     - 視覺階層和結構
   * 此清單檔案是下一步驟選擇適當範本的必要條件

3. **根據範本清單建立簡報大綱**：
   * 從步驟 2 檢視可用的範本。
   * 為第一張投影片選擇簡介或標題範本。這應該是最前面的範本之一。
   * 為其他投影片選擇安全、以文字為主的版面配置。
   * **關鍵：將版面配置結構與實際內容相符**：
     - 單欄版面配置：用於統一敘述或單一主題
     - 雙欄版面配置：僅在您有恰好 2 個不同項目/概念時使用
     - 三欄版面配置：僅在您有恰好 3 個不同項目/概念時使用
     - 圖片 + 文字版面配置：僅在您有實際圖片要插入時使用
     - 引用版面配置：僅用於來自人物的實際引用（附註明出處），絕不用於強調
     - 絕不使用佔位符號多於您的內容的版面配置
     - 如果您有 2 個項目，不要強行塞入 3 欄版面配置
     - 如果您有 4 個以上的項目，考慮分成多張投影片或使用清單格式
   * 在選擇版面配置之前先計算您的實際內容數量
   * 驗證所選版面配置中的每個佔位符號都會填入有意義的內容
   * 為每個內容區段選擇代表**最佳**版面配置的一個選項。
   * 儲存 `outline.md`，包含內容和利用可用設計的範本對應
   * 範本對應範例：
      ```
      # 要使用的範本投影片（從 0 開始的索引）
      # 警告：驗證索引在範圍內！有 73 張投影片的範本其索引為 0-72
      # 對應：大綱中的投影片編號 -> 範本投影片索引
      template_mapping = [
          0,   # 使用投影片 0（標題/封面）
          34,  # 使用投影片 34（B1：標題和內文）
          34,  # 再次使用投影片 34（為第二個 B1 複製）
          50,  # 使用投影片 50（E1：引用）
          54,  # 使用投影片 54（F2：結尾 + 文字）
      ]
      ```

4. **使用 `rearrange.py` 複製、重新排序和刪除投影片**：
   * 使用 `scripts/rearrange.py` 腳本以所需順序建立新簡報：
     ```bash
     python scripts/rearrange.py template.pptx working.pptx 0,34,34,50,52
     ```
   * 此腳本會自動處理重複投影片的複製、刪除未使用的投影片和重新排序
   * 投影片索引從 0 開始（第一張投影片是 0，第二張是 1，依此類推）
   * 同一個投影片索引可以出現多次以複製該投影片

5. **使用 `inventory.py` 腳本擷取所有文字**：
   * **執行清單擷取**：
     ```bash
     python scripts/inventory.py working.pptx text-inventory.json
     ```
   * **閱讀 text-inventory.json**：閱讀整個 text-inventory.json 檔案以了解所有圖形及其屬性。**閱讀此檔案時絕不設定任何範圍限制。**

   * 清單 JSON 結構：
      ```json
        {
          "slide-0": {
            "shape-0": {
              "placeholder_type": "TITLE",  // or null for non-placeholders
              "left": 1.5,                  // position in inches
              "top": 2.0,
              "width": 7.5,
              "height": 1.2,
              "paragraphs": [
                {
                  "text": "Paragraph text",
                  // Optional properties (only included when non-default):
                  "bullet": true,           // explicit bullet detected
                  "level": 0,               // only included when bullet is true
                  "alignment": "CENTER",    // CENTER, RIGHT (not LEFT)
                  "space_before": 10.0,     // space before paragraph in points
                  "space_after": 6.0,       // space after paragraph in points
                  "line_spacing": 22.4,     // line spacing in points
                  "font_name": "Arial",     // from first run
                  "font_size": 14.0,        // in points
                  "bold": true,
                  "italic": false,
                  "underline": false,
                  "color": "FF0000"         // RGB color
                }
              ]
            }
          }
        }
      ```

   * 主要功能：
     - **投影片**：命名為 "slide-0"、"slide-1" 等。
     - **圖形**：按視覺位置（從上到下、從左到右）排序為 "shape-0"、"shape-1" 等。
     - **佔位符號類型**：TITLE、CENTER_TITLE、SUBTITLE、BODY、OBJECT 或 null
     - **預設字型大小**：從版面配置佔位符號擷取的 `default_font_size`（以點為單位）（如有）
     - **投影片編號已過濾**：具有 SLIDE_NUMBER 佔位符號類型的圖形會自動從清單中排除
     - **項目符號**：當 `bullet: true` 時，`level` 始終會包含（即使為 0）
     - **間距**：`space_before`、`space_after` 和 `line_spacing` 以點為單位（僅在設定時包含）
     - **色彩**：RGB 使用 `color`（例如 "FF0000"），主題色彩使用 `theme_color`（例如 "DARK_1"）
     - **屬性**：僅包含非預設值於輸出中

6. **產生替換文字並將資料儲存至 JSON 檔案**
   根據上一步驟的文字清單：
   - **關鍵**：首先驗證清單中存在哪些圖形 - 僅引用實際存在的圖形
   - **驗證**：replace.py 腳本會驗證替換 JSON 中的所有圖形都存在於清單中
     - 如果您引用不存在的圖形，您會收到顯示可用圖形的錯誤
     - 如果您引用不存在的投影片，您會收到指示投影片不存在的錯誤
     - 所有驗證錯誤會在腳本退出前一次顯示
   - **重要**：replace.py 腳本在內部使用 inventory.py 來識別所有文字圖形
   - **自動清除**：清單中的所有文字圖形都會被清除，除非您為它們提供 "paragraphs"
   - 為需要內容的圖形新增 "paragraphs" 欄位（不是 "replacement_paragraphs"）
   - 替換 JSON 中沒有 "paragraphs" 的圖形會自動清除其文字
   - 具有項目符號的段落會自動靠左對齊。當 `"bullet": true` 時不要設定 `alignment` 屬性
   - 為佔位文字產生適當的替換內容
   - 使用圖形大小來決定適當的內容長度
   - **關鍵**：包含原始清單中的段落屬性 - 不要只提供文字
   - **重要**：當 bullet: true 時，不要在文字中包含項目符號（•、-、*）- 它們會自動新增
   - **基本格式規則**：
     - 標題/抬頭通常應有 `"bold": true`
     - 清單項目應有 `"bullet": true, "level": 0`（當 bullet 為 true 時，level 是必要的）
     - 保留任何對齊屬性（例如，`"alignment": "CENTER"` 用於置中文字）
     - 當與預設值不同時包含字型屬性（例如，`"font_size": 14.0`、`"font_name": "Lora"`）
     - 色彩：RGB 使用 `"color": "FF0000"`，主題色彩使用 `"theme_color": "DARK_1"`
     - 替換腳本期望**正確格式化的段落**，而非只是文字字串
     - **重疊圖形**：偏好具有較大 default_font_size 或更適當 placeholder_type 的圖形
   - 將含替換內容的更新清單儲存至 `replacement-text.json`
   - **警告**：不同的範本版面配置具有不同的圖形數量 - 在建立替換前務必檢查實際清單

   顯示正確格式的段落欄位範例：
   ```json
   "paragraphs": [
     {
       "text": "新簡報標題文字",
       "alignment": "CENTER",
       "bold": true
     },
     {
       "text": "區段標題",
       "bold": true
     },
     {
       "text": "第一個項目符號要點（不含項目符號）",
       "bullet": true,
       "level": 0
     },
     {
       "text": "紅色文字",
       "color": "FF0000"
     },
     {
       "text": "主題色彩文字",
       "theme_color": "DARK_1"
     },
     {
       "text": "無特殊格式的一般段落文字"
     }
   ]
   ```

   **替換 JSON 中未列出的圖形會自動清除**：
   ```json
   {
     "slide-0": {
       "shape-0": {
         "paragraphs": [...] // 此圖形會獲得新文字
       }
       // 清單中的 shape-1 和 shape-2 會自動清除
     }
   }
   ```

   **簡報的常見格式模式**：
   - 標題投影片：粗體文字，有時置中
   - 投影片內的區段標題：粗體文字
   - 項目符號清單：每個項目需要 `"bullet": true, "level": 0`
   - 內文文字：通常不需要特殊屬性
   - 引用：可能有特殊的對齊或字型屬性

7. **使用 `replace.py` 腳本應用替換**
   ```bash
   python scripts/replace.py working.pptx replacement-text.json output.pptx
   ```

   腳本將會：
   - 首先使用 inventory.py 的函式擷取所有文字圖形的清單
   - 驗證替換 JSON 中的所有圖形都存在於清單中
   - 清除清單中識別的所有圖形的文字
   - 僅對替換 JSON 中定義了 "paragraphs" 的圖形應用新文字
   - 透過應用 JSON 中的段落屬性來保留格式
   - 自動處理項目符號、對齊、字型屬性和色彩
   - 儲存更新的簡報

   驗證錯誤範例：
   ```
   ERROR: Invalid shapes in replacement JSON:
     - Shape 'shape-99' not found on 'slide-0'. Available shapes: shape-0, shape-1, shape-4
     - Slide 'slide-999' not found in inventory
   ```

   ```
   ERROR: Replacement text made overflow worse in these shapes:
     - slide-0/shape-2: overflow worsened by 1.25" (was 0.00", now 1.25")
   ```

## 建立縮圖網格

為快速分析和參考建立 PowerPoint 投影片的視覺縮圖網格：

```bash
python scripts/thumbnail.py template.pptx [output_prefix]
```

**功能**：
- 建立：`thumbnails.jpg`（大型簡報會建立 `thumbnails-1.jpg`、`thumbnails-2.jpg` 等）
- 預設：5 欄，每個網格最多 30 張投影片（5×6）
- 自訂前綴：`python scripts/thumbnail.py template.pptx my-grid`
  - 注意：如果您想在特定目錄中輸出，輸出前綴應包含路徑（例如 `workspace/my-grid`）
- 調整欄數：`--cols 4`（範圍：3-6，影響每個網格的投影片數）
- 網格限制：3 欄 = 12 張投影片/網格，4 欄 = 20，5 欄 = 30，6 欄 = 42
- 投影片索引從 0 開始（投影片 0、投影片 1 等）

**使用案例**：
- 範本分析：快速了解投影片版面配置和設計模式
- 內容審查：整個簡報的視覺概覽
- 導覽參考：根據視覺外觀找到特定投影片
- 品質檢查：驗證所有投影片的格式是否正確

**範例**：
```bash
# 基本用法
python scripts/thumbnail.py presentation.pptx

# 組合選項：自訂名稱、欄數
python scripts/thumbnail.py template.pptx analysis --cols 4
```

## 將投影片轉換為圖片

要視覺化分析 PowerPoint 投影片，使用兩步驟流程將它們轉換為圖片：

1. **將 PPTX 轉換為 PDF**：
   ```bash
   soffice --headless --convert-to pdf template.pptx
   ```

2. **將 PDF 頁面轉換為 JPEG 圖片**：
   ```bash
   pdftoppm -jpeg -r 150 template.pdf slide
   ```
   這會建立如 `slide-1.jpg`、`slide-2.jpg` 等檔案。

選項：
- `-r 150`：設定解析度為 150 DPI（調整以平衡品質/大小）
- `-jpeg`：輸出 JPEG 格式（如偏好 PNG 則使用 `-png`）
- `-f N`：要轉換的第一頁（例如 `-f 2` 從第 2 頁開始）
- `-l N`：要轉換的最後一頁（例如 `-l 5` 在第 5 頁停止）
- `slide`：輸出檔案的前綴

特定範圍的範例：
```bash
pdftoppm -jpeg -r 150 -f 2 -l 5 template.pdf slide  # 僅轉換第 2-5 頁
```

## 程式碼風格指南
**重要**：產生 PPTX 操作的程式碼時：
- 撰寫簡潔的程式碼
- 避免冗長的變數名稱和多餘的操作
- 避免不必要的 print 陳述式

## 相依套件

必要的相依套件（應已安裝）：

- **markitdown**：`pip install "markitdown[pptx]"`（用於從簡報擷取文字）
- **pptxgenjs**：`npm install -g pptxgenjs`（用於透過 html2pptx 建立簡報）
- **playwright**：`npm install -g playwright`（用於 html2pptx 中的 HTML 渲染）
- **react-icons**：`npm install -g react-icons react react-dom`（用於圖示）
- **sharp**：`npm install -g sharp`（用於 SVG 點陣化和圖片處理）
- **LibreOffice**：`sudo apt-get install libreoffice`（用於 PDF 轉換）
- **Poppler**：`sudo apt-get install poppler-utils`（用於 pdftoppm 將 PDF 轉換為圖片）
- **defusedxml**：`pip install defusedxml`（用於安全的 XML 解析）