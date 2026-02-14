# Copilot カスタム指示 — sample-app

## プロジェクト概要

sample-app は pioyan が開発するサンプルプロジェクトです。

## リポジトリ構成

```
.devcontainer/
└── devcontainer.json    # Dev Container 設定（gh CLI・推奨拡張）
.github/
├── agents/              # Custom Agents（Repo Guardian・Code Reviewer・Docs Writer）
├── skills/              # Agent Skills（監査・適用・CI・Dependabot・Git ワークフロー）
├── policies/            # 組織ポリシー文書（チェックリスト・ツール一覧）
├── workflows/           # GitHub Actions CI
├── ISSUE_TEMPLATE/      # Issue テンプレート
├── CODEOWNERS           # コードオーナー
├── dependabot.yml       # 依存自動更新
└── PULL_REQUEST_TEMPLATE.md
.vscode/
├── settings.json        # エージェント・Hooks 設定
├── extensions.json      # 推奨拡張機能
└── mcp.json             # ローカル MCP サーバー設定
```

## コーディング規約

- コミットメッセージは Conventional Commits に従う
- ブランチ名は `<type>/<short-description>` 形式
- PR は必ずテンプレートに従い、CI を通過させてからレビューを依頼する

## ビルド・テスト

<!-- TODO: 技術スタック確定後に具体的なコマンドを追記 -->

## CI

PR を作成すると以下の衛生チェックが自動実行されます:

- **actionlint**: GitHub Actions の静的解析
- **markdownlint**: Markdown の品質チェック
- **yamllint**: YAML の構文チェック
- **gitleaks**: シークレット漏洩検知
- **typos**: 誤字検知

## 開発環境

### Dev Container

`.devcontainer/devcontainer.json` で統一された開発環境を提供します:

- **ベースイメージ**: Microsoft Universal Image（言語非依存）
- **GitHub CLI**: `gh` コマンドが利用可能（初回は `gh auth login` で認証）
- **Docker**: MCP サーバー等の実行に必要な Docker が利用可能
- **推奨拡張**: コンテナ起動時に自動インストール

### Copilot Hooks

`.vscode/settings.json` で以下のフックが設定されています:

- **postSave**: `.md` ファイル保存時に markdownlint、`.yml`/`.yaml` ファイル保存時に yamllint を自動実行
- **postCommand**: コード変更後に typos チェックを自動実行

コード生成・編集のたびに品質チェックが自動で走るため、手動での lint 実行は不要です。

### サブエージェント連携

`chat.customAgentInSubagent.enabled: true` が有効化されており、
メインエージェントから以下のカスタムエージェントをサブエージェントとして呼び出すことができます。

## カスタムエージェント

このリポジトリには以下のカスタムエージェントが定義されています:

| エージェント | 用途 |
|------------|------|
| `@repo-guardian` | リポジトリのベストプラクティス準拠を監査し、不足分を PR で追加 |
| `@code-reviewer` | PR の差分をレビューし、品質・セキュリティ観点でコメントを提案 |
| `@docs-writer` | コード変更に伴うドキュメント更新提案を生成 |

## Agent Skills

このリポジトリには以下の Agent Skills が含まれています:

- `/repo-audit` — リポジトリのベストプラクティス準拠状況を監査
- `/repo-apply-baseline` — 不足ファイルを追加する
- `/ci-hygiene` — CI 衛生チェックの導入手順
- `/dependabot-baseline` — Dependabot の最小構成導入手順
- `/git-workflow` — Git 運用の標準手順（ブランチ・コミット・PR・rebase・hotfix・release）

Git の運用を指示された場合は、まず `/git-workflow` スキルを参照してください。
