---
name: task
description: "[number] Notion task. Lists if omitted."
---

## Arguments

```
/task [id]
```

No argument: query the Notion task database for open tasks, fetch linked GitHub Issues and PRs, display as a status-grouped tree, then exit.

With argument: fetch the task by page ID and resume work. Keep Notion status in sync throughout.

## Skills

Invoke via the Skill tool.

- notion-tasks-system: Task properties, status transitions, and formatting rules.
- gh-issue-template: Issue template, labels, and formatting rules.
- gh-pr-template: PR template, formatting, and required sections.
- .agent-browser: Browser automation for verification.
- .docs-update: Sync product specifications with code changes.
- commit-commands: Commit, push, and open PRs.

## Team

Create a team named `task-{id}` and delegate work to teammates. This saves context in the main session.

| Role | Name | subagent_type | Purpose |
|---|---|---|---|
| Planner | `task-{id}-planner` | `planner-task` | Plan phase. Investigate codebase, create GitHub Issue, sync Notion status. |
| Hacker | `task-{id}-hacker` | `hacker` | Security testing on localhost after implementation. |
| Code Debugger | `task-{id}-debugger-code` | `debugger-code` | Find code bugs and quality issues. |
| Docs Debugger | `task-{id}-debugger-docs` | `debugger-docs` | Find doc inconsistencies. |

## Exit conditions

Report to the user and exit when any of these is reached:

- Complete: no more work to do. Report a summary and add a Notion comment.
- Blocked: problem encountered. Present the cause and options. Add a Notion comment.
- Cancelled: user requested stop. Report the reason. Add a Notion comment.

## Workflow

### Tree display (no argument)

Fetch open tasks from Notion ordered by priority, then fetch linked GitHub Issues and PRs for each task.

Group by Notion status and display as a tree. Skip statuses with no tasks.

```
`作業待ち`

├─ #[**1042**](https://notion.so/...) 求人検索フィルターの改善
│  ├─ #[**91**](https://github.com/.../issues/91) ページネーション不具合
│  │  └─ #[**112**](https://github.com/.../pull/112) fix: オフセット修正
│  └─ #[**94**](https://github.com/.../issues/94) 文字数カウント不具合
│
└─ #[**1031**](https://notion.so/...) 企業プロフィール画像のリサイズ対応
   └─ #[**87**](https://github.com/.../issues/87) リダイレクト不具合
      └─ #[**113**](https://github.com/.../pull/113) fix: リダイレクト先を修正

`計画確認待ち`

└─ #[**1038**](https://notion.so/...) マッチング通知のリアルタイム化
```

Rules:

- Status as inline code header, blank line after
- `#` outside the link; number bold and linked to Notion or GitHub URL
- Issues indented under their parent task with `├─` / `└─`
- PRs indented under their parent issue with further indent
- Empty `│` line between task groups for readability

Exit after display.

### Plan phase

Set Notion status to "Planning". Spawn `task-{id}-planner` and pass the Notion task context. Prompt must include: "Plan this single task only. Do not loop to other issues." The planner investigates the codebase, creates a linked GitHub Issue with Technical Challenges and Plan, and adds a brief note to the Notion task. Wait for the planner to finish. Set Notion status to "Planning Review".

### Approval gate

Present the plan to the user and ask for approval.

- Approved: set Notion status to "Ready" and proceed.
- Rejected: set Notion status to "Planning Cancelled" and exit.

### Code phase

Set Notion status to "In Progress (Claude)". Implement changes following the task list in the issue. Check off tasks as completed. Commit as needed.

### Security phase (optional)

If the changes involve user input, authentication, or data handling, spawn `task-{id}-hacker` to run security testing on localhost.

### Verification

Before marking as complete, create a verification checklist covering all changes made. Use `.agent-browser` to verify each item by actually operating the application in the browser. All items must pass before proceeding.

### Docs update

Invoke `.docs-update` to sync product specifications in `.docs/` with the changes made. Commit the doc updates.

### Completion

Create a PR linking the issue. Set Notion status to "Review".

### Debug phase

After completion, spawn `task-{id}-debugger-code` and `task-{id}-debugger-docs` in parallel. They fix trivial issues on the spot and return non-trivial findings.

### Triage

Review findings from debuggers and triage each one. Ask the user how to handle each finding:

| Effort | Action |
|---|---|
| Trivial (typo, format) | Fix immediately and commit |
| Small, no planning needed | Create a new ticket (.claude/tickets/) |
| Needs planning | Create a new GitHub Issue |
| Large, needs stakeholder input | Create a new Notion task |

Maximum level for this skill: Notion task.

### Loop

After triage, if new items were created, pick the next actionable item and repeat from the Plan phase. Exit when there is nothing left to do. Shut down teammates.
