# Copilot カスタム指示 — pio-chat

## プロジェクト概要

pio-chat は pioyan が開発するチャットプロジェクトです。

## リポジトリ構成

```
.github/
├── agents/          # Custom Agents（Repo Guardian 等）
├── skills/          # Agent Skills（監査・適用・CI・Dependabot）
├── policies/        # 組織ポリシー文書（チェックリスト・ツール一覧）
├── workflows/       # GitHub Actions CI
├── ISSUE_TEMPLATE/  # Issue テンプレート
├── CODEOWNERS       # コードオーナー
├── dependabot.yml   # 依存自動更新
└── PULL_REQUEST_TEMPLATE.md
.vscode/
└── mcp.json         # ローカル MCP サーバー設定
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

## Agent Skills

このリポジトリには以下の Agent Skills が含まれています:

- `/repo-audit` — リポジトリのベストプラクティス準拠状況を監査
- `/repo-apply-baseline` — 不足ファイルを追加する
- `/ci-hygiene` — CI 衛生チェックの導入手順
- `/dependabot-baseline` — Dependabot の最小構成導入手順
