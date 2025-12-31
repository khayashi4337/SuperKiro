# SuperKiro 🚀

> チーム開発のためのナレッジ蓄積・仕様駆動開発支援 Kiro Power
>
> Inspired by [SuperClaude](https://github.com/NickBusey/SuperClaude)

## Overview

SuperKiroは、開発チームの「調べ直し」「聞き直し」を撲滅するKiro Powerです。

- ✅ トラブルシューティングの自動記録
- ✅ PRレビュー指摘の事前チェック
- ✅ フェーズ/イテレーション管理（Phase/Stage/SubStage階層構造）
- ✅ チームナレッジの資産化
- ✅ AI可読なドキュメント設計

## Quick Links

| ドキュメント | 内容 |
|--------------|------|
| [QuickStart.md](./QuickStart.md) | 5分で始めるガイド |
| [Onboarding.md](./Onboarding.md) | 新メンバー向け運用ガイド |
| [FAQ.md](./FAQ.md) | よくある質問 |
| [BestPractices.md](./BestPractices.md) | 大規模プロジェクト向けTips |

### 運用チェックリスト

| ドキュメント | 対象 | 内容 |
|--------------|------|------|
| [member-checklist.md](./docs/_templates/member-checklist.md) | メンバー | PR作成前/タスク完了時/週次チェック |
| [leader-checklist.md](./docs/_templates/leader-checklist.md) | リーダー | 運用状況の確認・メンバーフォロー |

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
├── QuickStart.md         # クイックスタートガイド
├── FAQ.md                # よくある質問
├── BestPractices.md      # 大規模プロジェクト向けTips
├── steering/             # ステアリングファイル
│   ├── coding-standards.md
│   ├── initial-setup.md
│   ├── project-profile.md
│   ├── review-rules.md
│   ├── knowledge-workflow.md
│   ├── project-structure.md  # Phase/Stage/SubStage階層定義
│   └── current-stage.md      # 現在位置の追跡
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
    ├── learning/         # 振り返り
    └── design/           # 設計ドキュメント
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

#### `docs/design/`（設計ドキュメント）

- 何を書くか: artifacts分類定義、AI可読ドキュメントガイド
- 参照:
  - `docs/design/artifacts.md` - AS-IS/TO-BE等の成果物分類
  - `docs/design/ai-readable-docs.md` - AI時代のドキュメント設計ガイド

## Usage

SuperKiroは「同じことを二度調べない」ために、以下の3つの記録を推奨しています。

### 1. トラブルシューティング記録

**目的**: エラーを解決したら記録し、次に同じ問題が起きたときに即座に解決できるようにする

**いつ書く？**: バグ修正、エラー解決、ハマりポイントを乗り越えたとき

```markdown
# docs/troubleshooting/2025-01-15-prisma-connection.md

## 症状
Prisma Client が接続プールを使い果たす

## 原因
開発サーバーのホットリロードで接続が蓄積

## 解決方法
prisma.ts で singleton パターンを使用
```

### 2. レビュー指摘の蓄積

**目的**: PRレビューで受けた指摘を記録し、次回から同じ指摘を受けないようにする

**いつ書く？**: レビューで指摘を受けたとき、または自分で「これは他の人もやりそう」と思ったとき

```markdown
# docs/reviews/tags/error-handling.md

## try-catch の空キャッチ
- 指摘: catchブロックが空
- 対策: 最低限 console.error を入れる
```

### 3. イテレーション記録（機能の変更履歴）

**目的**: 機能の変更履歴を Before/After で記録し、「なぜこうなっているか」を後から追跡できるようにする

**いつ書く？**: 機能を追加・改善したとき（PRマージ後など）

**イテレーションとは？**: 機能のバージョンアップの記録です。v0.1 → v0.2 → v0.3 と改善を重ねる様子を残します。

```markdown
# docs/features/user-auth/iterations/v0.2-oauth-added.md

## Before
- メール+パスワードのみ
- 離脱率: 35%

## After
- Google/GitHub OAuth追加
- 離脱率: 18%

## 学び
- OAuth導入でUXが大幅改善
- 次はパスワードレス認証を検討
```

---

## PR運用ワークフロー

PRベースで開発している場合の推奨ワークフローです。

### PRを作る前

**目的**: 過去の指摘を確認し、同じミスを繰り返さない

1. `docs/reviews/tags/` を確認（同じ指摘を繰り返さないため）
2. 変更が機能単位なら、該当の `docs/features/{feature}/` を更新
3. 変更が大きい場合は、イテレーション記録を残す

### レビューで指摘を受けたら

**目的**: 指摘を資産化し、チーム全体の品質向上につなげる

1. 指摘が汎用的なら `docs/reviews/tags/{category}.md` に追記
2. 頻出化しているなら `steering/review-rules.md` にも反映

### マージ後

**目的**: 解決した問題や得た知見を記録し、チームで共有する

1. 解決した問題があれば `docs/troubleshooting/` に残す
2. 再利用できる実装なら `docs/patterns/` に残す
3. 変更点の意図・影響を `docs/features/{feature}/changelog.md` に残す

---

## 新機能追加の流れ

新しい機能を追加するときの推奨手順です。

### Step 1: 仕様（Spec）を用意

Kiroの仕様駆動開発に従い、まず仕様を定義します。

```text
.kiro/specs/{feature}/requirements.md  # 要件定義
.kiro/specs/{feature}/design.md        # 設計書
```

### Step 2: Featureドキュメントの雛形を作成

```text
docs/features/user-auth/README.md              # 機能の概要
docs/features/user-auth/changelog.md           # 変更履歴
docs/features/user-auth/iterations/v0.1-initial.md  # 最初のイテレーション
```

テンプレート: `docs/_templates/feature/`, `docs/_templates/iteration.md`

### Step 3: 実装中に起きた問題を記録

```text
docs/troubleshooting/YYYY-MM-DD-{issue-name}.md
```

### Step 4: 実装完了時にイテレーション記録を更新

`docs/_templates/iteration.md` を参考に、以下を記録:

- Before / After（何が変わったか）
- テスト結果
- 学び（次に活かせること）
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
