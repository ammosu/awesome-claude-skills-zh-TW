---
name: ax-extract-workflow
description: 當使用者想知道特定 PR、功能、報告、交付物、日期或 commit sha 是如何產出，並需要用本地 ax 歷史還原工作流程時使用。
---

# ax-extract-workflow

使用本地 `ax` 歷史，還原某個具體交付物背後的有序工作流程。這是唯讀流程：檢查 sessions、commits、skill 使用和 subagent 活動，然後用證據在對話中直接回答。

## 前置條件

- `ax` 可從 `PATH` 執行。
- 本地 ax database 或 daemon 正在運作。
- 盡可能從相關 git repository 內執行指令。

如果 `ax` 無法連上 database，請告訴使用者先啟動 ax database 或 daemon，然後暫停這次 extraction workflow，直到 ax 可用為止。不要編造缺失的歷史。

## 解析錨點

依照使用者提供的資訊選擇模式：

| 使用者輸入 | 模式 | 動作 |
| --- | --- | --- |
| `commit sha` | sha | 直接使用該 sha。 |
| `YYYY-MM-DD` 或日期範圍 | date | 使用 `ax sessions around <date>`。 |
| topic、PR、功能或 artifact 名稱 | topic | 執行 `ax recall "<topic>" --sources=commit --json`，選出最佳 commit 候選。 |
| 「這個 repo 最近」 | pwd | 使用 `ax sessions here --days=14`。 |

如果 topic 結果不明確，先請使用者選擇錨點，再繼續。

## 界定 sessions 範圍

依照解析出的錨點執行對應指令：

- sha: `ax sessions near <sha> --json`
- date: `ax sessions around <date> --days=3 --json`
- pwd: `ax sessions here --days=14 --json`

選出最相關的 sessions，通常最多五個。優先挑選 turns 較多，且接觸到該 artifact 相關 files、commits 或 topics 的 sessions。

## 檢查 sessions

對每個選出的 session 執行：

```bash
ax sessions show <id> --json
ax sessions show <id> --by-role
```

使用 `top_skills`、skill roles、file 與 commit references，以及 `agent_delegations`。如果某個 subagent 的工作對 artifact 很關鍵，深入查看：

```bash
ax sessions show <id> --expand=<subagent-uuid>
```

使用 `ax recall "<keyword>" --json` 找出使用者的方向決策或重要摘錄。如果本地 ax 版本支援 skill filter，可加上 `--skill=<skill-name>`。

## 回答格式

在對話中直接回傳還原結果：

1. 摘要：還原了哪個 artifact，以及使用了哪個錨點。
2. 使用的證據：session IDs、commits、dates，以及任何展開的 subagents。
3. 有序工作流程：依序列出 skills、tools 和 subagents，並為每一步寫出一個具體產出。
4. 關鍵決策：列出二到四個改變方向的 turns 或摘錄，並附上引用來源。
5. 重現簡報：只有在使用者詢問如何重複該流程時才提供。

## 守則

- 不要寫入檔案或修改 repository。
- 證據不完整時，明確標出不確定性。
- 如果 `ax sessions show <id> --by-role` 回傳許多未分類 skills，回答後再建議執行 `ax skills classify`。不要因此阻塞還原工作。
