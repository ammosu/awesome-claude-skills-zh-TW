<h1 align="center">Awesome Claude Skills</h1>

<p align="center">
  繁體中文 | <a href="README.en.md">English</a>
</p>

<p align="center">
<a href="https://platform.composio.dev/?utm_source=Github&utm_medium=Youtube&utm_campaign=2025-11&utm_content=AwesomeSkills">
  <img width="1280" height="640" alt="Composio banner" src="https://github.com/user-attachments/assets/adb3f57a-2706-4329-856f-059a32059d48">
</a>


</p>

<p align="center">
  <a href="https://awesome.re">
    <img src="https://awesome.re/badge.svg" alt="Awesome" />
  </a>
  <a href="https://makeapullrequest.com">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square" alt="PRs Welcome" />
  </a>
  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=flat-square" alt="License: Apache-2.0" />
  </a>
</p>
<div>
<p align="center">
  <a href="https://twitter.com/composio">
    <img src="https://img.shields.io/badge/Follow on X-000000?style=for-the-badge&logo=x&logoColor=white" alt="Follow on X" />
  </a>
  <a href="https://www.linkedin.com/company/composiohq/">
    <img src="https://img.shields.io/badge/Follow on LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="Follow on LinkedIn" />
  </a>
  <a href="https://discord.com/invite/composio">
    <img src="https://img.shields.io/badge/Join our Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Join our Discord" />
  </a>
  </p>
</div>

精選實用 Claude Skills 清單，用於提升 Claude.ai、Claude Code 和 Claude API 的生產力。


> 如果您希望您的技能能夠跨 500+ 應用程式採取行動，請使用 [Composio](https://platform.composio.dev/?utm_source=Github&utm_medium=Youtube&utm_campaign=2025-11&utm_content=AwesomeSkills) 整合


## 目錄

- [什麼是 Claude Skills？](#什麼是-claude-skills)
- [技能清單](#技能清單)
  - [文件處理](#文件處理)
  - [開發與程式工具](#開發與程式工具)
  - [資料與分析](#資料與分析)
  - [商業與行銷](#商業與行銷)
  - [溝通與寫作](#溝通與寫作)
  - [創意與媒體](#創意與媒體)
  - [生產力與組織](#生產力與組織)
  - [協作與專案管理](#協作與專案管理)
  - [安全性與系統](#安全性與系統)
- [開始使用](#開始使用)
- [創建技能](#創建技能)
- [貢獻](#貢獻)
- [資源](#資源)
- [授權](#授權)

## 什麼是 Claude Skills？

- [mblode/agent-skills](https://github.com/mblode/agent-skills) - Nobody ships AI slop on purpose. These skills make sure you don't. UI audits, typography, docs, PR review, and releases. `npx skills add mblode/agent-skills`
Claude Skills 是可自訂的工作流程，可教導 Claude 如何根據您的獨特需求執行特定任務。Skills 使 Claude 能夠在所有 Claude 平台上以可重複、標準化的方式執行任務。

## 技能清單

### 文件處理

- [docx](https://github.com/anthropics/skills/tree/main/document-skills/docx) - 建立、編輯、分析 Word 文件，支援追蹤修訂、註解、格式設定。
- [pdf](https://github.com/anthropics/skills/tree/main/document-skills/pdf) - 提取文字、表格、中繼資料，合併與註釋 PDF。
- [pptx](https://github.com/anthropics/skills/tree/main/document-skills/pptx) - 讀取、生成和調整投影片、版面配置、範本。
- [xlsx](https://github.com/anthropics/skills/tree/main/document-skills/xlsx) - 試算表操作：公式、圖表、資料轉換。
- [Markdown to EPUB Converter](https://github.com/smerchek/claude-epub-skill) - 將 Markdown 文件和聊天摘要轉換為專業的 EPUB 電子書檔案。*By [@smerchek](https://github.com/smerchek)*

### 開發與程式工具

- [artifacts-builder](https://github.com/anthropics/skills/tree/main/web-artifacts-builder) - 用於建立精緻、多組件 claude.ai HTML artifacts 的工具套件，使用現代前端網頁技術（React、Tailwind CSS、shadcn/ui）。
- [aws-skills](https://github.com/zxkane/aws-skills) - AWS 開發，包含 CDK 最佳實踐、成本優化 MCP 伺服器以及無伺服器/事件驅動架構模式。
- [Changelog Generator](./changelog-generator/) - 透過分析歷史記錄並將技術提交轉換為客戶友善的發布說明，自動從 git 提交建立面向使用者的變更日誌。
- [Claude Code Terminal Title](https://github.com/bluzername/claude-code-terminal-title) - 為每個 Claude Code 終端視窗提供動態標題，描述正在執行的工作，以便您不會忘記哪個視窗在做什麼。
- [D3.js Visualization](https://github.com/chrisvoncsefalvay/claude-d3js-skill) - 教導 Claude 製作 D3 圖表和互動式資料視覺化。*By [@chrisvoncsefalvay](https://github.com/chrisvoncsefalvay)*
- [FFUF Web Fuzzing](https://github.com/jthack/ffuf_claude_skill) - 整合 ffuf 網頁模糊測試工具，讓 Claude 能夠執行模糊測試任務並分析漏洞結果。*By [@jthack](https://github.com/jthack)*
- [finishing-a-development-branch](https://github.com/obra/superpowers/tree/main/skills/finishing-a-development-branch) - 透過呈現清晰的選項並處理所選工作流程來指導開發工作的完成。
- [iOS Simulator](https://github.com/conorluddy/ios-simulator-skill) - 使 Claude 能夠與 iOS 模擬器互動，用於測試和除錯 iOS 應用程式。*By [@conorluddy](https://github.com/conorluddy)*
- [MCP Builder](./mcp-builder/) - 指導建立高品質的 MCP（Model Context Protocol）伺服器，用於使用 Python 或 TypeScript 將外部 API 和服務與 LLM 整合。
- [move-code-quality-skill](https://github.com/1NickPappas/move-code-quality-skill) - 針對官方 Move Book Code Quality Checklist 分析 Move 語言套件，檢查 Move 2024 Edition 合規性和最佳實踐。
- [Playwright Browser Automation](https://github.com/lackeyjb/playwright-skill) - 模型呼叫的 Playwright 自動化，用於測試和驗證 Web 應用程式。*By [@lackeyjb](https://github.com/lackeyjb)*
- [prompt-engineering](https://github.com/NeoLabHQ/context-engineering-kit/tree/master/plugins/customaize-agent/skills/prompt-engineering) - 教導知名的提示工程技術和模式，包括 Anthropic 最佳實踐和代理說服原則。
- [pypict-claude-skill](https://github.com/omkamal/pypict-claude-skill) - 使用 PICT（Pairwise Independent Combinatorial Testing）為需求或程式碼設計全面的測試案例，生成具有成對覆蓋率的優化測試套件。
- [Skill Creator](./skill-creator/) - 提供建立有效 Claude Skills 的指導，透過專業知識、工作流程和工具整合來擴展能力。
- [Skill Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) - 在幾分鐘內自動將任何文件網站轉換為 Claude AI 技能。*By [@yusufkaraaslan](https://github.com/yusufkaraaslan)*
- [software-architecture](https://github.com/NeoLabHQ/context-engineering-kit/tree/master/plugins/ddd/skills/software-architecture) - 實作設計模式，包括 Clean Architecture、SOLID 原則和全面的軟體設計最佳實踐。
- [subagent-driven-development](https://github.com/NeoLabHQ/context-engineering-kit/tree/master/plugins/sadd/skills/subagent-driven-development) - 為個別任務調度獨立的子代理，在迭代之間設置程式碼審查檢查點，實現快速、受控的開發。
- [test-driven-development](https://github.com/obra/superpowers/tree/main/skills/test-driven-development) - 在實作任何功能或錯誤修復時使用，在編寫實作程式碼之前。
- [using-git-worktrees](https://github.com/obra/superpowers/blob/main/skills/using-git-worktrees/) - 建立隔離的 git worktree，具有智慧目錄選擇和安全驗證。
- [Webapp Testing](./webapp-testing/) - 使用 Playwright 測試本地 Web 應用程式，用於驗證前端功能、除錯 UI 行為和擷取螢幕截圖。

### 資料與分析

- [CSV Data Summarizer](https://github.com/coffeefuelbump/csv-data-summarizer-claude-skill) - 自動分析 CSV 檔案並生成包含視覺化的綜合見解，無需使用者提示。*By [@coffeefuelbump](https://github.com/coffeefuelbump)*
- [root-cause-tracing](https://github.com/obra/superpowers/tree/main/skills/root-cause-tracing) - 當錯誤在執行深處發生時使用，您需要追溯尋找原始觸發器。

### 商業與行銷

- [Brand Guidelines](./brand-guidelines/) - 將 Anthropic 的官方品牌色彩和字體應用於 artifacts，以實現一致的視覺識別和專業設計標準。
- [Competitive Ads Extractor](./competitive-ads-extractor/) - 從廣告庫中提取和分析競爭對手的廣告，以了解引起共鳴的訊息和創意方法。
- [Domain Name Brainstormer](./domain-name-brainstormer/) - 生成創意網域名稱構想，並檢查多個頂級網域（包括 .com、.io、.dev 和 .ai 擴充名）的可用性。
- [Internal Comms](./internal-comms/) - 協助撰寫內部溝通，包括 3P 更新、公司通訊、FAQ、狀態報告和專案更新，使用公司特定格式。
- [Lead Research Assistant](./lead-research-assistant/) - 透過分析您的產品、搜尋目標公司並提供可行的外展策略來識別和評估高品質潛在客戶。

### 溝通與寫作

- [article-extractor](https://github.com/michalparkola/tapestry-skills-for-claude-code/tree/main/article-extractor) - 從網頁中提取完整的文章文字和中繼資料。
- [brainstorming](https://github.com/obra/superpowers/tree/main/skills/brainstorming) - 透過結構化提問和替代方案探索，將粗略的想法轉化為完整的設計。
- [Content Research Writer](./content-research-writer/) - 透過進行研究、新增引用、改進吸睛開場和提供逐節回饋來協助撰寫高品質內容。
- [family-history-research](https://github.com/emaynard/claude-family-history-research-skill) - 協助規劃家族歷史和家譜研究專案。
- [Meeting Insights Analyzer](./meeting-insights-analyzer/) - 分析會議記錄以揭示行為模式，包括衝突迴避、發言比例、填充詞和領導風格。
- [NotebookLM Integration](https://github.com/PleasePrompto/notebooklm-skill) - 讓 Claude Code 直接與 NotebookLM 聊天，根據上傳的文件獲取基於來源的答案。*By [@PleasePrompto](https://github.com/PleasePrompto)*

### 創意與媒體

- [Canvas Design](./canvas-design/) - 使用設計哲學和美學原則在 PNG 和 PDF 文件中建立精美的視覺藝術，用於海報、設計和靜態作品。
- [Image Enhancer](./image-enhancer/) - 透過增強解析度、銳利度和清晰度來提高圖像和螢幕截圖品質，用於專業簡報和文件。
- [Slack GIF Creator](./slack-gif-creator/) - 建立針對 Slack 優化的動畫 GIF，具有大小限制驗證器和可組合的動畫基元。
- [Theme Factory](./theme-factory/) - 將專業字體和色彩主題應用於 artifacts，包括投影片、文件、報告和 HTML 登陸頁面，提供 10 種預設主題。
- [Video Downloader](./video-downloader/) - 從 YouTube 和其他平台下載影片，用於離線觀看、編輯或存檔，支援各種格式和品質選項。
- [youtube-transcript](https://github.com/michalparkola/tapestry-skills-for-claude-code/tree/main/youtube-transcript) - 從 YouTube 影片獲取字幕並準備摘要。

### 生產力與組織

- [File Organizer](./file-organizer/) - 透過理解上下文、尋找重複項目並建議更好的組織結構來智慧地組織檔案和資料夾。
- [Invoice Organizer](./invoice-organizer/) - 透過讀取檔案、提取資訊並一致地重新命名，自動組織發票和收據以進行稅務準備。
- [kaizen](https://github.com/NeoLabHQ/context-engineering-kit/tree/master/plugins/kaizen/skills/kaizen) - 應用持續改進方法論，採用多種分析方法，基於日本改善哲學和精實方法論。
- [n8n-skills](https://github.com/haunchen/n8n-skills) - 使 AI 助理能夠直接理解和操作 n8n 工作流程。
- [Raffle Winner Picker](./raffle-winner-picker/) - 從清單、試算表或 Google Sheets 隨機選擇贈品和競賽的獲勝者，具有加密安全的隨機性。
- [ship-learn-next](https://github.com/michalparkola/tapestry-skills-for-claude-code/tree/main/ship-learn-next) - 協助迭代接下來要建立或學習什麼的技能，基於回饋循環。
- [tapestry](https://github.com/michalparkola/tapestry-skills-for-claude-code/tree/main/tapestry) - 將相關文件互連並摘要成知識網路。

### 協作與專案管理

- [git-pushing](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/git-pushing) - 自動化 git 操作和儲存庫互動。
- [review-implementing](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/review-implementing) - 評估程式碼實作計劃並與規格對齊。
- [test-fixing](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/engineering-workflow-plugin/skills/test-fixing) - 檢測失敗的測試並提議修補程式或修復。

### 安全性與系統

- [computer-forensics](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/computer-forensics-skills/skills/computer-forensics) - 數位鑑識分析和調查技術。
- [file-deletion](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/computer-forensics-skills/skills/file-deletion) - 安全檔案刪除和資料清理方法。
- [metadata-extraction](https://github.com/mhattingpete/claude-skills-marketplace/tree/main/computer-forensics-skills/skills/metadata-extraction) - 提取和分析檔案中繼資料以進行鑑識。
- [threat-hunting-with-sigma-rules](https://github.com/jthack/threat-hunting-with-sigma-rules-skill) - 使用 Sigma 偵測規則來追蹤威脅並分析安全事件。

## 開始使用

### 在 Claude.ai 中使用技能

1. 在聊天介面中點擊技能圖示（🧩）。
2. 從市集新增技能或上傳自訂技能。
3. Claude 會根據您的任務自動啟用相關技能。

### 在 Claude Code 中使用技能

1. 將技能放置在 `~/.config/claude-code/skills/`：
   ```bash
   mkdir -p ~/.config/claude-code/skills/
   cp -r skill-name ~/.config/claude-code/skills/
   ```

2. 驗證技能中繼資料：
   ```bash
   head ~/.config/claude-code/skills/skill-name/SKILL.md
   ```

3. 啟動 Claude Code：
   ```bash
   claude
   ```

4. 技能會自動載入並在相關時啟用。

### 透過 API 使用技能

使用 Claude Skills API 以程式化方式載入和管理技能：

```python
import anthropic

client = anthropic.Anthropic(api_key="your-api-key")

response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    skills=["skill-id-here"],
    messages=[{"role": "user", "content": "Your prompt"}]
)
```

詳細資訊請參閱 [Skills API 文件](https://docs.claude.com/en/api/skills-guide)。

## 創建技能

### 技能結構

每個技能都是一個包含 `SKILL.md` 檔案的資料夾，並帶有 YAML frontmatter：

```
skill-name/
├── SKILL.md          # 必需：技能說明和中繼資料
├── scripts/          # 可選：輔助腳本
├── templates/        # 可選：文件範本
└── resources/        # 可選：參考檔案
```

### 基本技能範本

```markdown
---
name: my-skill-name
description: 清楚描述此技能的功能以及何時使用。
---

# My Skill Name

技能目的和能力的詳細說明。

## 何時使用此技能

- 使用案例 1
- 使用案例 2
- 使用案例 3

## 說明

[關於如何執行此技能的 Claude 詳細說明]

## 範例

[展示技能實際應用的真實範例]
```

### 技能最佳實踐

- 專注於特定、可重複的任務
- 包含清楚的範例和邊界情況
- 為 Claude 而非終端使用者編寫說明
- 跨 Claude.ai、Claude Code 和 API 進行測試
- 記錄先決條件和相依性
- 包含錯誤處理指導

## 貢獻

我們歡迎貢獻！請閱讀我們的[貢獻指南](CONTRIBUTING.md)了解以下詳細資訊：

- 如何提交新技能
- 技能品質標準
- Pull request 流程
- 行為準則

### 快速貢獻步驟

1. 確保您的技能基於真實使用案例
2. 檢查現有技能中是否有重複項目
3. 遵循技能結構範本
4. 跨平台測試您的技能
5. 提交具有清楚文件的 pull request

## 資源

### 官方文件

- [Claude Skills 概述](https://www.anthropic.com/news/skills) - 官方公告和功能
- [Skills 使用者指南](https://support.claude.com/en/articles/12512180-using-skills-in-claude) - 如何在 Claude 中使用技能
- [建立自訂技能](https://support.claude.com/en/articles/12512198-creating-custom-skills) - 技能開發指南
- [Skills API 文件](https://docs.claude.com/en/api/skills-guide) - API 整合指南
- [Agent Skills 部落格文章](https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) - 工程深度探討

### 社群資源

- [Anthropic Skills 儲存庫](https://github.com/anthropics/skills) - 官方範例技能
- [Claude 社群](https://community.anthropic.com) - 與其他使用者討論技能
- [Skills 市集](https://claude.ai/marketplace) - 發現和分享技能

### 靈感與使用案例

- [Lenny's Newsletter](https://www.lennysnewsletter.com/p/everyone-should-be-using-claude-code) - 50 種人們使用 Claude Code 的方式
- [Notion Skills](https://www.notion.so/notiondevs/Notion-Skills-for-Claude-28da4445d27180c7af1df7d8615723d0) - Notion 整合技能


## 加入社群

- 對於將 Composio 與您的認證設定整合有疑問嗎？[與我們快速通話](https://calendly.com/thomas-composio/composio-enterprise-setup)
- [在 Twitter 上關注我們](https://x.com/composio)
- [加入我們的 Discord](https://discord.com/invite/composio)

## 授權

本儲存庫採用 Apache License 2.0 授權。

個別技能可能有不同的授權 - 請查看每個技能資料夾以獲取特定的授權資訊。

---

**注意**：Claude Skills 可跨 Claude.ai、Claude Code 和 Claude API 使用。一旦您建立了一個技能，它就可以跨所有平台移植，使您的工作流程在使用 Claude 的任何地方都保持一致。
