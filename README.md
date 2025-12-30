# SuperKiro 🚀

> チーム開発のためのナレッジ蓄積・仕様駆動開発支援 Kiro Power
> 
> Inspired by [SuperClaude](https://github.com/NickBusey/SuperClaude)

## Overview

SuperKiroは、開発チームの「調べ直し」「聞き直し」を撲滅するKiro Powerです。

- ✅ トラブルシューティングの自動記録
- ✅ PRレビュー指摘の事前チェック
- ✅ フェーズ/イテレーション管理
- ✅ チームナレッジの資産化

## Installation

### Kiro IDE

1. Kiro IDEで `Manage Powers` を開く
2. `Add power from GitHub` をクリック
3. このリポジトリのURLを入力

### Manual

```bash
git clone https://github.com/YOUR_USERNAME/SuperKiro.git
cd SuperKiro

# プロジェクトにコピー
cp -r steering/* YOUR_PROJECT/.kiro/steering/
cp -r hooks/* YOUR_PROJECT/.kiro/hooks/
cp -r docs/* YOUR_PROJECT/docs/
```

## Directory Structure

```
SuperKiro/
├── POWER.md              # Kiro Power エントリーポイント
├── README.md             # このファイル
├── steering/             # ステアリングファイル
│   ├── coding-standards.md
│   ├── review-rules.md
│   └── knowledge-workflow.md
├── hooks/                # 自動化フック
│   ├── troubleshooting-logger.json
│   └── review-checker.json
└── docs/                 # ナレッジ蓄積テンプレート
    ├── _templates/       # 各種テンプレート
    ├── project/phases/   # フェーズ管理
    ├── features/         # 機能別ドキュメント
    ├── troubleshooting/  # エラー解決記録
    ├── reviews/tags/     # レビュー指摘パターン
    ├── patterns/         # 実装パターン
    ├── libraries/        # ライブラリTips
    └── learning/         # 振り返り
```

## Usage

### トラブルシューティングを記録

```markdown
# docs/troubleshooting/2025-01-15-prisma-connection.md

## 症状
Prisma Client が接続プールを使い果たす

## 原因
開発サーバーのホットリロードで接続が蓄積

## 解決方法
prisma.ts で singleton パターンを使用
```

### レビュー指摘を蓄積

```markdown
# docs/reviews/tags/error-handling.md

## try-catch の空キャッチ
- 指摘: catchブロックが空
- 対策: 最低限 console.error を入れる
```

### イテレーション記録

```markdown
# docs/features/user-auth/iterations/v0.2-oauth-added.md

## Before
- メール+パスワードのみ
- 離脱率: 35%

## After  
- Google/GitHub OAuth追加
- 離脱率: 18%
```

## Hooks

| Hook | Trigger | Description |
|------|---------|-------------|
| troubleshooting-logger | File save | エラー修正時に自動記録を促す |
| review-checker | File save | レビュー頻出指摘を事前チェック |

## Customization

1. `steering/coding-standards.md` をプロジェクトの規約に編集
2. `steering/review-rules.md` にチーム固有の指摘パターンを追加
3. `docs/_templates/` のテンプレートを必要に応じてカスタマイズ

## Philosophy

> 「解決したらすぐ書く」を自動化で強制する

完璧なドキュメントより、書かれたドキュメント。
「たぶんキャッシュ関連。あとで調べる」でも価値がある。

## License

MIT

## Contributing

PRs welcome! 特に以下を歓迎します：

- 新しいテンプレート
- 便利なHooks
- ベストプラクティスの追加
