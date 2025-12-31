---
name: "superkiro"
displayName: "SuperKiro - Team Knowledge Management"
description: "チーム開発のためのナレッジ蓄積・仕様駆動開発支援Power。トラブルシューティング、レビュー指摘、Phase/Stage/SubStage階層管理を自動化"
keywords: ["knowledge", "documentation", "troubleshooting", "review", "iteration", "phase", "stage", "substage", "team", "docs", "ナレッジ", "ドキュメント", "大規模プロジェクト"]
---

# SuperKiro - Team Knowledge Management Power

SuperKiroは、チーム開発におけるナレッジ蓄積と仕様駆動開発を支援するKiro Powerです。

## What This Power Does

- **ナレッジの自動蓄積**: トラブルシューティング、レビュー指摘、実装パターンを構造化して蓄積
- **Phase/Stage/SubStage管理**: 大規模プロジェクトの階層的な進行管理
- **AI可読ドキュメント**: Kiroが理解しやすい構造化されたドキュメント設計
- **自動化Hooks**: エラー解決時の自動記録、レビュー指摘の事前チェック

## Quick Links

| ドキュメント | 内容 |
|--------------|------|
| [QuickStart.md](./QuickStart.md) | 5分で始めるガイド |
| [Onboarding.md](./Onboarding.md) | 新メンバー向け運用ガイド |
| [FAQ.md](./FAQ.md) | よくある質問 |
| [BestPractices.md](./BestPractices.md) | 大規模プロジェクト向けTips |

### 運用チェックリスト

| ドキュメント | 対象 |
|--------------|------|
| [member-checklist.md](./docs/_templates/member-checklist.md) | メンバー向け（PR作成前/週次） |
| [leader-checklist.md](./docs/_templates/leader-checklist.md) | リーダー向け（運用状況確認） |

## Onboarding

### Step 1: Validate project structure

プロジェクトに `docs/` ディレクトリが存在するか確認してください。
存在しない場合は、このPowerの `docs/` ディレクトリをプロジェクトにコピーしてください。

### Step 2: Copy steering files

`steering/` ディレクトリの内容を `.kiro/steering/` にコピーしてください。
既存のsteeringファイルがある場合はマージしてください。

初回は以下も実施してください。

1. `steering/initial-setup.md` に沿ってヒアリング
2. `steering/project-profile.md` に回答を残す

### Step 3: Install hooks

`hooks/` ディレクトリのJSONファイルを `.kiro/hooks/` にコピーしてください。

```bash
cp -r steering/* .kiro/steering/
cp -r hooks/* .kiro/hooks/
cp -r docs/* docs/
```

### Step 4: Customize for your project

`steering/coding-standards.md` をプロジェクトの規約に合わせて編集してください。
レビュー方式に合わせて、`steering/review-rules.md` も調整してください。

## Workflows

### When solving an error

1. エラーを解決したら、`docs/troubleshooting/YYYY-MM-DD-{issue}.md` を作成
2. Hookが有効な場合は自動で記録を促します
3. テンプレート: `docs/_templates/troubleshooting.md`

### When receiving PR review feedback

1. `docs/reviews/tags/{category}.md` に指摘パターンを追記
2. `steering/review-rules.md` に頻出指摘を反映
3. 次回から同じ指摘を事前回避

### When completing an iteration

1. `docs/features/{feature}/iterations/v{X}.{Y}-{description}.md` を作成
2. Before/After、テスト結果、学びを記録
3. テンプレート: `docs/_templates/iteration.md`

### When completing a phase (大規模プロジェクト向け)

1. `docs/project/phases/phase-{N}-{name}/retrospective.md` を作成
2. Keep/Problem/Try を記録
3. 次フェーズへの申し送りを明記
4. `steering/current-stage.md` を更新

## Phase/Stage/SubStage 階層管理

大規模プロジェクト向けの階層的な進行管理機能です。

```
Phase (大分類: プロジェクトの大きな区切り)
└── Stage (中分類: 目的別の作業単位)
    └── SubStage (小分類: 具体的なタスク群)
        └── Feature (実装単位: PR単位)
```

### 関連ファイル

| ファイル | 役割 |
|----------|------|
| `steering/project-structure.md` | 階層構造の定義 |
| `steering/current-stage.md` | 現在位置の追跡 |
| `docs/_templates/phase/_phase.md` | Phase用テンプレート |
| `docs/_templates/phase/_stage.md` | Stage用テンプレート |
| `docs/_templates/phase/_substage.md` | SubStage用テンプレート |
| `docs/design/artifacts.md` | 成果物分類（AS-IS/TO-BE等） |
| `docs/design/ai-readable-docs.md` | AI可読ドキュメントガイド |

## Best Practices

- **完璧を求めない**: 「たぶんキャッシュ関連。あとで調べる」でもOK。書かないより書く。
- **Before/Afterを必ず書く**: 過去の修正パターンをKiroが学習できる
- **週次振り返り**: 毎週15分、`docs/learning/weekly-retrospective.md` を更新
- **リンクを活用**: `[[troubleshooting/xxx]]` で関連ドキュメントを参照
- **AI可読形式**: Markdown + YAML frontmatter で構造化

詳細は [BestPractices.md](./BestPractices.md) を参照してください。

## Directory Structure

```
project-root/
├── .kiro/
│   ├── steering/           # SuperKiroのsteering
│   │   ├── project-structure.md  # 階層構造定義
│   │   └── current-stage.md      # 現在位置追跡
│   ├── hooks/              # SuperKiroのhooks
│   └── specs/              # Kiro自動生成の仕様書
│
└── docs/                   # ナレッジ蓄積
    ├── _templates/         # テンプレート集
    │   └── phase/          # Phase/Stage/SubStage用
    ├── project/            # プロジェクト全体管理
    │   └── phases/         # フェーズ別進捗
    ├── features/           # 機能別ドキュメント
    ├── troubleshooting/    # エラー解決記録
    ├── reviews/tags/       # レビュー指摘パターン
    ├── patterns/           # 実装パターン集
    ├── libraries/          # ライブラリ使用方法
    ├── learning/           # 振り返り・学習記録
    └── design/             # 設計ドキュメント
        ├── artifacts.md    # 成果物分類定義
        └── ai-readable-docs.md  # AI可読ドキュメントガイド
```
