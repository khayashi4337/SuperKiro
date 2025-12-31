# FAQ

## 基本

### Q: SuperKiroとは何ですか？

チーム開発のナレッジを蓄積・再利用するためのKiro Powerです。「同じ問題を何度も調べる」「同じ指摘を何度も受ける」を防ぎます。

### Q: 最低限何をすればいいですか？

1. `steering/project-profile.md` にプロジェクト情報を記入
2. エラーを解決したら `docs/troubleshooting/` に記録
3. レビュー指摘を受けたら `docs/reviews/tags/` に記録

これだけで十分価値があります。

### Q: 完璧に書かなくてもいいですか？

**はい**。「たぶんキャッシュ関連。あとで調べる」でも価値があります。書かれたドキュメント > 完璧なドキュメント。

---

## Kiroエージェント

### Q: Kiroにはエージェント機能がありますか？

**はい**。Kiroには以下のエージェント機能があります:

| 機能 | 説明 |
|------|------|
| **Autonomous Agent** | セッションを超えてコンテキストを維持。フィードバックを記憶して次回に適用 |
| **Agent Hooks** | ファイル保存時に自動実行。テスト更新、README更新、セキュリティスキャン等 |
| **Kiro Powers** | 拡張機能。steering + hooks + MCP servers をパッケージ化（SuperKiroはこれ） |
| **Kiro CLI** | ターミナルでも同じエージェントを利用可能 |

参考: [Introducing Kiro autonomous agent](https://kiro.dev/blog/introducing-kiro-autonomous-agent/)

### Q: ルールが多くて覚えられません

**覚える必要はありません**。`steering/` にルールを書いておけば、Kiroのエージェントが参照して従ってくれます。

SuperKiroの構成がそのままエージェントをサポートする仕組みになっています:

```
SuperKiro/
├── steering/     ← AIへの指示（エージェントが参照）
├── hooks/        ← 自動化（エージェントが実行）
└── docs/         ← ナレッジ（エージェントが学習）
```

### Q: エージェントにドキュメント形式を守らせたい

`steering/` にルールを追加すれば、エージェントが自動的に従います。AI可読なドキュメント形式については `docs/design/ai-readable-docs.md` を参照してください。

### Q: Kiro PowerでPythonスクリプトを実行できますか？

**はい、Hooks経由で実行可能です。**

Kiro Hooksは以下の2種類のアクションを実行できます:

| アクションタイプ | 説明 |
|------------------|------|
| Agent Prompt | AIエージェントへの指示（自然言語） |
| Shell Command | シェルコマンド実行（Pythonスクリプト含む） |

例:
```json
{
  "name": "run-python-check",
  "trigger": "file_saved",
  "pattern": "**/*.py",
  "action": {
    "type": "shell",
    "command": "python scripts/check.py $FILE"
  }
}
```

### Q: Kiro Powersの構成要素は何ですか？

| 要素 | 内容 |
|------|------|
| MCP Server | 外部ツール連携 |
| Steering Files | AIへのルール定義（Markdown） |
| Hooks | 自動化トリガー（JSON） |

参考: [Hooks - Kiro Docs](https://kiro.dev/docs/hooks/)

### Q: Hooksのトリガータイプは？

| イベント | 用途例 |
|----------|--------|
| ファイル保存時 | Lint実行、テスト更新 |
| 新規ファイル作成時 | テンプレート適用 |
| ファイル削除時 | 関連ファイル整理 |
| プロンプト送信時 | 入力チェック |
| エージェント完了時 | 結果検証 |

---

## ディレクトリ構造

### Q: どこに何を書けばいいですか？

| 書きたいこと | 置き場所 |
|--------------|----------|
| エラー解決の記録 | `docs/troubleshooting/` |
| レビュー指摘パターン | `docs/reviews/tags/` |
| 再利用できる実装パターン | `docs/patterns/` |
| ライブラリの使い方 | `docs/libraries/` |
| 機能単位のドキュメント | `docs/features/{feature}/` |
| フェーズ管理 | `docs/project/phases/` |
| 下書き・検討中 | `docs/draft/` |

### Q: `steering/` と `docs/` の違いは？

| ディレクトリ | 目的 |
|--------------|------|
| `steering/` | AIへの指示・プロジェクト設定 |
| `docs/` | ナレッジ蓄積・成果物 |

---

## Phase/Stage/SubStage

### Q: Phase/Stage/SubStageとは何ですか？

プロジェクトを階層的に分割する仕組みです:

```
Phase (大分類: プロジェクトの大きな区切り)
└── Stage (中分類: 目的別の作業単位)
    └── SubStage (小分類: 具体的なタスク群)
        └── Feature (実装単位: PR単位)
```

### Q: 必ず使う必要がありますか？

**いいえ**。小規模プロジェクトなら不要です。大規模・長期プロジェクトで段階的に進める場合に有効です。

### Q: AS-IS と TO-BE の違いは？

| 種類 | 内容 |
|------|------|
| `as-is-source.md` | ソースコードから読み取った現行仕様 |
| `as-is-behavior.md` | 動作テストで判明した実際の挙動 |
| `to-be.md` | あるべき姿・確定要件 |
| `interview-notes.md` | ヒアリング議事録 |

詳細: `docs/design/artifacts.md`

### Q: 今どこにいるか分からなくなったら？

`steering/current-stage.md` を確認・更新してください。

---

## カスタマイズ

### Q: テンプレートを変更したい

`docs/_templates/` 配下のファイルを編集してください。

### Q: チーム固有のルールを追加したい

`steering/review-rules.md` に追記してください。

### Q: Hooksを無効化したい

`hooks/` 配下の該当JSONファイルを削除または名前変更してください。

---

## トラブルシューティング

### Q: どのテンプレートを使えばいいか分からない

| 状況 | テンプレート |
|------|--------------|
| Phase全体の目標設定 | `docs/_templates/phase/_phase.md` |
| Stage単位の指示 | `docs/_templates/phase/_stage.md` |
| SubStage単位のタスク | `docs/_templates/phase/_substage.md` |
| 機能のREADME | `docs/_templates/feature/README.md` |
| エラー解決記録 | `docs/_templates/troubleshooting.md` |

### Q: ファイルが増えすぎて管理できない

- 古いPhaseのドキュメントはアーカイブを検討
- `docs/draft/` の整理を定期的に実施
- 命名規則を統一（日付prefix推奨: `YYYY-MM-DD-`）
