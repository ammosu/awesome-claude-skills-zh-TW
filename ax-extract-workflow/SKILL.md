---
name: ax-extract-workflow
description: Use when the user asks how a specific PR, feature, report, shipped artifact, date, or commit was produced and local ax history should be used to reconstruct the workflow.
---

# ax-extract-workflow

Use local `ax` history to reconstruct the ordered work that produced a specific artifact. This is a read-only workflow: inspect sessions, commits, skill usage, and subagent activity, then answer inline with evidence.

## Preconditions

- `ax` is available on `PATH`.
- The local ax database or daemon is running.
- Run commands from the relevant git repository when possible.

If `ax` cannot connect to its database, tell the user to start the ax database or daemon, then stop this extraction workflow until ax is available. Do not invent missing history.

## Resolve the anchor

Choose the mode from what the user gave you:

| User input | Mode | Action |
| --- | --- | --- |
| `commit sha` | sha | Use it directly. |
| `YYYY-MM-DD` or date range | date | Use `ax sessions around <date>`. |
| topic, PR, feature, or artifact name | topic | Run `ax recall "<topic>" --sources=commit --json` and choose the best commit candidate. |
| "this repo recently" | pwd | Use `ax sessions here --days=14`. |

If topic results are ambiguous, ask the user to pick an anchor before continuing.

## Window sessions

Run the command that matches the resolved anchor:

- sha: `ax sessions near <sha> --json`
- date: `ax sessions around <date> --days=3 --json`
- pwd: `ax sessions here --days=14 --json`

Select the most relevant sessions, usually up to five. Prioritize sessions with higher turn counts and sessions that touch files, commits, or topics related to the artifact.

## Inspect sessions

For each selected session, run:

```bash
ax sessions show <id> --json
ax sessions show <id> --by-role
```

Use `top_skills`, skill roles, file and commit references, and `agent_delegations`. If a subagent's work looks central to the artifact, drill in:

```bash
ax sessions show <id> --expand=<subagent-uuid>
```

Use `ax recall "<keyword>" --json` to find user steering decisions or important excerpts. If the local ax version supports skill filtering, add `--skill=<skill-name>`.

## Answer format

Return the reconstruction inline:

1. Summary: what artifact was reconstructed and which anchor was used.
2. Evidence used: session IDs, commits, dates, and any expanded subagents.
3. Ordered workflow: skills, tools, and subagents in sequence, with one concrete result per step.
4. Key decisions: two to four cited turns or excerpts that changed direction.
5. Reproducer brief: only if the user asks how to repeat the workflow.

## Guardrails

- Do not write files or modify the repository.
- Keep uncertainty explicit when evidence is partial.
- If `ax sessions show <id> --by-role` returns many unclassified skills, suggest `ax skills classify` after answering. Do not block on classification.
