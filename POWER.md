---
name: "superkiro"
displayName: "SuperKiro - Team Knowledge Management"
description: "チーム開発のためのナレッジ蓄積・仕様駆動開発支援Power。トラブルシューティング、レビュー指摘、イテレーション管理を自動化"
keywords: ["knowledge", "documentation", "troubleshooting", "review", "iteration", "phase", "team", "docs", "ナレッジ", "ドキュメント"]
---

# SuperKiro - Team Knowledge Management Power

SuperKiroは、チーム開発におけるナレッジ蓄積と仕様駆動開発を支援するKiro Powerです。

## What This Power Does

- **ナレッジの自動蓄積**: トラブルシューティング、レビュー指摘、実装パターンを構造化して蓄積
- **フェーズ管理**: プロジェクトの段階的進行を goals / decisions / retrospective で追跡
- **イテレーション記録**: 機能別の Before/After、学びを記録
- **自動化Hooks**: エラー解決時の自動記録、レビュー指摘の事前チェック

## Onboarding

### Step 1: Validate project structure

プロジェクトに `docs/` ディレクトリが存在するか確認してください。
存在しない場合は、このPowerの `docs/` ディレクトリをプロジェクトにコピーしてください。

### Step 2: Copy steering files

`steering/` ディレクトリの内容を `.kiro/steering/` にコピーしてください。
既存のsteeringファイルがある場合はマージしてください。

### Step 3: Install hooks

`hooks/` ディレクトリのJSONファイルを `.kiro/hooks/` にコピーしてください。

```bash
cp -r steering/* .kiro/steering/
cp -r hooks/* .kiro/hooks/
cp -r docs/* docs/
```

### Step 4: Customize for your project

`steering/coding-standards.md` をプロジェクトの規約に合わせて編集してください。

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

### When completing a phase

1. `docs/project/phases/phase-{N}-{name}/retrospective.md` を作成
2. Keep/Problem/Try を記録
3. 次フェーズへの申し送りを明記

## Best Practices

- **完璧を求めない**: 「たぶんキャッシュ関連。あとで調べる」でもOK。書かないより書く。
- **Before/Afterを必ず書く**: 過去の修正パターンをKiroが学習できる
- **週次振り返り**: 毎週15分、`docs/learning/weekly-retrospective.md` を更新
- **リンクを活用**: `[[troubleshooting/xxx]]` で関連ドキュメントを参照

## Directory Structure

```
project-root/
├── .kiro/
│   ├── steering/           # SuperKiroのsteering
│   ├── hooks/              # SuperKiroのhooks
│   └── specs/              # Kiro自動生成の仕様書
│
└── docs/                   # ナレッジ蓄積
    ├── _templates/         # テンプレート集
    ├── project/            # プロジェクト全体管理
    │   └── phases/         # フェーズ別進捗
    ├── features/           # 機能別ドキュメント
    ├── troubleshooting/    # エラー解決記録
    ├── reviews/tags/       # レビュー指摘パターン
    ├── patterns/           # 実装パターン集
    ├── libraries/          # ライブラリ使用方法
    └── learning/           # 振り返り・学習記録
```
