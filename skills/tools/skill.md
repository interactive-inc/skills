---
name: tools
description: List all available tools in the current session, grouped by MCP server prefix.
when_to_use: Invoke when the user wants to inspect the tool definitions available in the current session, including MCP tools grouped by prefix.
metadata:
  description: 現在のセッションで利用可能な全ツール定義を参照して出力するスキル。MCP ツールはサーバープレフィックスでグループ化する。
  dev: true
---

ツール定義（システムから渡される関数スキーマ）を参照し出力する。

## 形式

- ツール名
- 説明（簡潔に）

MCP ツールはプレフィックスでグループ化して表示する（例: `mcp__claude-in-chrome__*` は「Claude in Chrome」グループ）。

## 注意事項

- ツール一覧はセッションごとに異なる可能性がある
- 設定（`.mcp.json` など）の変更でツールが増減する
- 実行環境や権限によって利用可能なツールが変わる
