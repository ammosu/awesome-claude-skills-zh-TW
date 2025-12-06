---
name: skill-share
description: 一個建立新 Claude skills 並使用 Rube 自動在 Slack 上分享它們的 skill，以實現無縫的團隊協作和 skill 發現。
license: 完整條款見 LICENSE.txt
---

## 何時使用此 Skill

當您需要以下功能時使用此 skill：
- **建立新的 Claude skills**，具有適當的結構和中繼資料
- **生成 skill 套件**，準備好進行分發
- **自動在 Slack 上分享建立的 skills**，以提高團隊能見度
- **在分享前驗證 skill 結構**
- **打包和分發** skills 給您的團隊

也可在以下情況使用此 skill：
- **使用者說他想要建立/分享他的 skill**

此 skill 非常適合：
- 作為團隊工作流程的一部分建立 skills
- 建構需要 skill 建立 + 團隊通知的內部工具
- 自動化 skill 開發流程
- 具有團隊通知的協作 skill 建立

## 主要功能

### 1. Skill 建立
- 建立具有 SKILL.md 的適當結構化 skill 目錄
- 生成標準化的 scripts/、references/ 和 assets/ 目錄
- 自動生成具有所需中繼資料的 YAML frontmatter
- 強制執行命名慣例（連字號格式）

### 2. Skill 驗證
- 驗證 SKILL.md 格式和必填欄位
- 檢查命名慣例
- 確保打包前的中繼資料完整性

### 3. Skill 打包
- 建立可分發的 zip 檔案
- 包含所有 skill 資產和文件
- 打包前自動執行驗證

### 4. 透過 Rube 整合 Slack
- 自動將建立的 skill 資訊傳送至指定的 Slack 頻道
- 分享 skill 中繼資料（名稱、描述、連結）
- 發布 skill 摘要以供團隊發現
- 提供 skill 檔案的直接連結

## 運作方式

1. **初始化**：提供 skill 名稱和描述
2. **建立**：以適當的結構建立 skill 目錄
3. **驗證**：驗證 skill 中繼資料的正確性
4. **打包**：將 skill 打包成可分發的格式
5. **Slack 通知**：將 skill 詳細資訊發布到您團隊的 Slack 頻道

## 使用範例

```
當您要求 Claude 建立名為「pdf-analyzer」的 skill 時：
1. 建立 /skill-pdf-analyzer/，包含 SKILL.md 範本
2. 生成結構化目錄（scripts/、references/、assets/）
3. 驗證 skill 結構
4. 將 skill 打包為 zip 檔案
5. 發布到 Slack：「已建立新 Skill：pdf-analyzer - 進階 PDF 分析和提取功能」
```

## 與 Rube 整合

此 skill 利用 Rube 進行：
- **SLACK_SEND_MESSAGE**：將 skill 資訊發布到團隊頻道
- **SLACK_POST_MESSAGE_WITH_BLOCKS**：分享豐富格式化的 skill 中繼資料
- **SLACK_FIND_CHANNELS**：發現 skill 公告的目標頻道

## 要求

- 透過 Rube 連接 Slack 工作區
- 對 skill 建立目錄的寫入存取權限
- Python 3.7+ 用於 skill 建立腳本
- skill 通知的目標 Slack 頻道
