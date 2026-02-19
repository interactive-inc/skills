---
name: gh-issue
description: GitHub Issue template and guidelines for creating issues
---

# GitHub Issue テンプレートとガイドライン

GitHub Issue は開発者が読む。技術的な内容（ファイル名、関数名、実装方針など）を記載する。

## Issue 本文テンプレート

すべての Issue に対応する Notion タスクが必要。Notion タスクの URL を本文冒頭に記載する。

```
[TASK-{番号}](https://www.notion.so/{ページID})

[問題の概要と技術的な背景を見出しなしで直接記述。影響するファイル・APIなど技術的な事実を書く]

## 対応内容

- [ ] 技術的なタスク1（例: auth.login.ts の Set-Cookie に Secure フラグを追加）
- [ ] 技術的なタスク2

## 備考

[実装上の注意点、参考コード、関連ファイル、ワークアラウンドなど]
```

## Labels のルール

| 種類 | Label | 説明 |
|---|---|---|
| バグ修正 | `bug` | 何かが正しく動作していない |
| 機能追加・機能修正 | `enhancement` | 新機能の追加、既存機能の改善 |
| ドキュメント | `documentation` | 仕様書、README、コメントの追加・修正 |
| リファクタリング | `refactoring` | 動作を変えずにコードを整理 |
| テスト | `testing` | テストの追加・修正 |
| セキュリティ | `security` | セキュリティ上の問題 |
| パフォーマンス | `performance` | パフォーマンス改善 |

複数のラベルを付与しても良い（例: `bug` + `security`）

## 重要な注意事項

- **全 Issue に Notion タスクが必要**: Notion タスクなしで Issue を作成しない（例外なし）
- **タイトルは `TASK-{Notionタスク番号} - {タイトル}` 形式**: 例 `TASK-852 - 認証 Cookie にセキュリティフラグが未設定`
- **本文冒頭に Notion タスク URL**: `[TASK-852](https://www.notion.so/...)` の形式で記載
- **技術的な内容を書く**: GitHub Issue は開発者向け。Notion タスクに書かない技術詳細（ファイル名・関数名・実装方針）をここに書く
- **適切なラベルを付与**: 上記のルールに従って分類する
- **対応内容はチェックリスト形式**: 実装すべき技術的な項目を明確にする
