---
name: backlog-planning
description: "Create or update product backlog content."
arguments: Issue description or backlogs/ slug.
metadata:
  author: shigurenimo
---

Receive discussion results and return drafted backlog content in the docs format.

Does not read or write files. Does not operate GitHub/Notion.

## Workflow

- Receive the discussion results from the backlog skill
- Read the docs skill to understand `.docs/` format
- Draft backlog content following the format
- Return the drafted content

## Plugins

Invoke via the Skill tool.

- docs: `.docs/` format and rules.
- superpowers: Spawn parallel agents, create plans, review code.
