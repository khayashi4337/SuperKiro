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

### 初回設定

プロジェクトの前提に合わせて、以下のファイル（コピー先: `YOUR_PROJECT/.kiro/steering/`）を編集する必要があります：
- `steering/project-profile.md`
- `steering/coding-standards.md`
- `steering/review-rules.md`

`steering/initial-setup.md` で初回設定を行うことで、チームの開発スタイルに合わせたルールを適用できます。

## Directory Structure

```
SuperKiro/
├── POWER.md              # Kiro Power エントリーポイント
├── README.md             # このファイル
├── steering/             # ステアリングファイル
│   ├── coding-standards.md
│   ├── initial-setup.md
│   ├── project-profile.md
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

### docs/ 配下フォルダの補足（何をどこに書くか）

`docs/` は「後から検索できる形で知見を残す」ための置き場所です。詳細な方針は `steering/knowledge-workflow.md` を参照してください。

#### `docs/drafts/`（下書き）

- 何を書くか: まだ完成していないアイデアや検討中の内容の下書き
- テンプレート: なし（自由記述）

#### `docs/project/phases/`（フェーズ管理）

- 何を書くか: フェーズ単位の目標/意思決定/振り返り（Keep/Problem/Try など）
- テンプレート: `docs/_templates/phase/`
- 例:

```text
docs/project/phases/phase-1-mvp/retrospective.md
```

#### `docs/patterns/`（実装パターン）

- 何を書くか: 再利用できる設計・実装の型、ハマりどころと回避策
- テンプレート: `docs/_templates/pattern.md`
- 例:

```text
docs/patterns/error-handling.md
```

#### `docs/libraries/`（ライブラリTips）

- 何を書くか: ライブラリの基本的な使い方、プロジェクト内の使用例、注意点
- テンプレート: `docs/_templates/library.md`
- 例:

```text
docs/libraries/react-hook-form.md
```

#### `docs/learning/`（振り返り・学び）

- 何を書くか: 週次/隔週の振り返り、学びの要約、次にやること
- テンプレート: `docs/_templates/weekly-retrospective.md`
- 例:

```text
docs/learning/weekly-retrospective.md
```

## Usage

### トラブルシューティングを記録する例

```markdown
# docs/troubleshooting/2025-01-15-prisma-connection.md

## 症状
Prisma Client が接続プールを使い果たす

## 原因
開発サーバーのホットリロードで接続が蓄積

## 解決方法
prisma.ts で singleton パターンを使用
```

### レビュー指摘を蓄積する例

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

### PRの運用例（チェック → レビュー知見化 → 次回改善）

#### PRを作る前（最低限）

1. `docs/reviews/tags/` を確認（同じ指摘を繰り返さないため）
2. 変更が機能単位なら、該当の `docs/features/{feature}/` を更新
3. 変更が大きい場合は、イテレーション記録を残す

例:

```text
docs/reviews/tags/react-hooks.md
docs/features/user-auth/README.md
docs/features/user-auth/changelog.md
docs/features/user-auth/iterations/v0.3-refresh-token.md
```

#### レビューで指摘を受けたら（次回の自動回避に繋げる）

1. 指摘が汎用的なら `docs/reviews/tags/{category}.md` に追記
2. 頻出化しているなら `steering/review-rules.md` にも反映

例（レビュー指摘の蓄積）:

````markdown
# docs/reviews/tags/naming.md

## 指摘: booleanの命名

### 問題のコード
```ts
const open = true;
```

### 修正後のコード
```ts
const isOpen = true;
```
````

#### マージ後（またはPR作成直前）

1. 解決した問題があれば `docs/troubleshooting/` に残す
2. 再利用できる実装なら `docs/patterns/` に残す
3. 変更点の意図・影響を `docs/features/{feature}/changelog.md` に残す

### 新機能を追加するときの手順例（Spec → 実装 → ドキュメント）

#### 1) 仕様（Spec）を用意

- `.kiro/specs/{feature}/requirements.md`
- `.kiro/specs/{feature}/design.md`

#### 2) Featureドキュメントの雛形を作成

テンプレート:

- `docs/_templates/feature/README.md`
- `docs/_templates/feature/changelog.md`
- `docs/_templates/iteration.md`

作成例:

```text
docs/features/user-auth/README.md
docs/features/user-auth/changelog.md
docs/features/user-auth/iterations/v0.1-initial.md
```

#### 3) 実装中に起きた問題は、その場で残す

```text
docs/troubleshooting/YYYY-MM-DD-{issue-name}.md
```

#### 4) 実装完了時にイテレーション記録を更新

`docs/_templates/iteration.md` に沿って、最低限以下を埋めるのがコツです。

- Before / After
- テスト結果
- 学び
- 発生した問題（`docs/troubleshooting/` へのリンク）

## Hooks

| Hook | Trigger | Description |
|------|---------|-------------|
| troubleshooting-logger | File save | エラー修正時に自動記録を促す |
| review-checker | File save | レビュー頻出指摘を事前チェック |

## Customization

1. `steering/initial-setup.md` を実施して、前提（言語/レビュー方式/運用方針）を整理
2. `steering/project-profile.md` に回答を残す
3. `steering/coding-standards.md` をプロジェクトの規約に編集
4. `steering/review-rules.md` にチーム固有の指摘パターンを追加
5. `docs/_templates/` のテンプレートを必要に応じてカスタマイズ

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
