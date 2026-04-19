---
name: issue-planning
description: "Create technical plan text for a GitHub Issue."
arguments: Issue 番号
metadata:
  author: shigurenimo
---

GitHub Issue の内容をもとにコードベースを読み、gh-issue-template に従った技術計画テキストを作成して返す。

GitHub の操作はしない。

## 手順

- `gh issue view {number}` で Issue の内容を取得する
- コードベースを読んで影響範囲を把握する
- `gh-issue-template` スキルのテンプレートに従って計画テキストを作成する
- テキストを返す

## スキップ基準

以下の場合は計画できない旨を返す:

- 要件が曖昧で複数の解釈がある
- 外部サービスや環境の情報が不足
- 別の Issue に依存している
- 技術的な不明点が多くリスクが高い

## Plugins

Invoke via the Skill tool.

- `gh-issue-template`: テンプレートとラベルのルール
- `superpowers`: Spawn parallel agents, create plans, review code.
