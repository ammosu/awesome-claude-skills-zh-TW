---
name: x-twitter-scraper
description: Use when a user needs structured X/Twitter data workflows for post search, profile context, engagement research, giveaways, or trend analysis with Xquik.
license: MIT
---

# x-twitter-scraper

Use this skill when a task needs repeatable X/Twitter data collection instead of manual browser copying.

## When to Use This Skill

- Search public X/Twitter posts and collect source URLs.
- Inspect public profile, follower, or engagement context.
- Prepare giveaway draw inputs or trend research.
- Hand structured results to another analysis, report, or monitoring workflow.

## What This Skill Does

1. Routes agents to the public Xquik skill and API docs.
2. Keeps the `XQUIK_API_KEY` in a local secret store or environment variable.
3. Uses public post URLs, handles, queries, and returned response fields as working context.
4. Requires explicit user approval before posting or account-changing actions.

## How to Use

### Install the Source Skill

Install from the public source repository:

```
https://github.com/Xquik-dev/x-twitter-scraper
```

### Read the Public Docs

- Product docs: https://docs.xquik.com
- API overview: https://docs.xquik.com/api-reference/overview
- MCP guide: https://docs.xquik.com/mcp/overview

## Example Prompts

```
Use x-twitter-scraper to collect source links for recent posts about this launch.
```

```
Search X/Twitter for posts about this keyword and summarize engagement signals.
```

```
Prepare public post URLs for a giveaway draw, then wait for approval before drawing.
```

## Safety Notes

- Do not ask users for X passwords, 2FA codes, cookies, or session exports.
- Do not paste API keys into prompts, public files, or chat logs.
- Confirm before any write, post, reply, follow, media upload, or account-changing workflow.
- Use only public docs and returned response fields when sharing results.

Xquik is an independent third-party service. Not affiliated with X Corp. "Twitter" and "X" are trademarks of X Corp.

**Source:** [Xquik-dev/x-twitter-scraper](https://github.com/Xquik-dev/x-twitter-scraper)
