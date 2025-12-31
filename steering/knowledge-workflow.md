# ナレッジ蓄積ワークフロー

SuperKiroにおけるナレッジ蓄積の基本ワークフローです。

## 基本原則

1. **解決したらすぐ書く** - 記憶が新しいうちに
2. **完璧を求めない** - 「たぶんキャッシュ関連」でもOK
3. **Before/Afterを必ず書く** - 過去パターンの検索性向上
4. **リンクで繋げる** - 関連ドキュメントへの参照

## いつ何を書くか

| タイミング | 書く場所 | テンプレート |
|-----------|---------|-------------|
| エラーを解決した | `docs/troubleshooting/` | `_templates/troubleshooting.md` |
| PRで指摘を受けた | `docs/reviews/tags/` | `_templates/review-tag.md` |
| 新ライブラリ導入 | `docs/libraries/` | `_templates/library.md` |
| 再利用パターン発見 | `docs/patterns/` | `_templates/pattern.md` |
| 機能を実装・変更 | `docs/features/` | `_templates/feature/` |
| フェーズ完了 | `docs/project/phases/` | `_templates/phase/` |
| 週次振り返り | `docs/learning/` | `_templates/weekly-retrospective.md` |

## ファイル命名規則

### トラブルシューティング
```
docs/troubleshooting/YYYY-MM-DD-{issue-name}.md
例: 2025-01-15-prisma-connection-pool.md
```

### イテレーション
```
docs/features/{feature}/iterations/v{X}.{Y}-{description}.md
例: docs/features/user-auth/iterations/v0.2-oauth-added.md
```

### フェーズ
```
docs/project/phases/phase-{N}-{name}/
例: docs/project/phases/phase-1-mvp/
```

## Kiro への指示

### トラブルシューティング記録時
エラーを解決したことを検知したら、以下を確認してください：
1. `docs/troubleshooting/` に類似の記録がないか検索
2. なければ新規作成を提案
3. テンプレート `docs/_templates/troubleshooting.md` を使用

### レビュー指摘記録時
PRレビューの指摘を受けたら：
1. `docs/reviews/tags/` から該当カテゴリを検索
2. なければカテゴリファイルを新規作成
3. `steering/review-rules.md` への反映も検討

### イテレーション記録時
機能の実装が完了したら：
1. `docs/features/{feature}/iterations/` に記録を作成
2. Before/After、テスト結果、学びを必ず含める
3. 発生した問題は `docs/troubleshooting/` へのリンクで参照

## 週次振り返り（推奨）

毎週金曜日に15分：

```markdown
# YYYY-Www 振り返り

## 今週学んだこと
-

## 今週解決した問題
- [[troubleshooting/xxx]]

## ドキュメント更新
- [x] troubleshootingに追記した
- [ ] 新しいパターンをpatternsに追記した
```

## 大規模プロジェクト向け: Phase/Stage/SubStage

レガシー移行や長期プロジェクトでは、階層的な進行管理が有効です。

```
Phase (大分類) → Stage (中分類) → SubStage (小分類) → Feature (PR単位)
```

### 関連ファイル

| ファイル | 役割 |
|----------|------|
| `steering/project-structure.md` | 階層構造の定義 |
| `steering/current-stage.md` | 現在位置の追跡 |
| `docs/_templates/phase/` | Phase/Stage/SubStage用テンプレート |
| `docs/design/artifacts.md` | 成果物分類（AS-IS/TO-BE等） |
| `docs/design/ai-readable-docs.md` | AI可読ドキュメントガイド |

### SubStage完了時の記録

各SubStage完了時に以下を作成:

| ファイル | 内容 |
|----------|------|
| `output.md` | 発見事項・次への申し送り |
| `artifacts/as-is-source.md` | ソースから読み取った仕様 |
| `artifacts/as-is-behavior.md` | 動作テストで判明した実態 |
| `artifacts/to-be.md` | 確定要件 |
| `artifacts/interview-notes.md` | ヒアリング議事録 |

詳細は [BestPractices.md](../BestPractices.md) を参照してください。
