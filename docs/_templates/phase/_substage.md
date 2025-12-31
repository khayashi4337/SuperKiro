# SubStage {{N}}: {{name}}

## 目的

<!-- このSubStageで達成すべきこと -->

## インプット

- 前提条件:
- 参照先: `../substage-{{N-1}}-xxx/output.md`
- 必要な資料:

## タスク

- [ ]
- [ ]

## アウトプット

完了時に以下を作成:

### output.md

- 発見事項
- 次SubStageへの申し送り

### artifacts/ （該当するもののみ）

| ファイル | 内容 | 情報源 |
|----------|------|--------|
| `as-is-source.md` | ソースコードから読み取った仕様 | コード解析 |
| `as-is-behavior.md` | 現行動作テストで判明した実態 | 入出力テスト |
| `to-be.md` | 確定した要件 | 正式ドキュメント |
| `interview-notes.md` | ヒアリング議事録・部分的要望 | 顧客MTG |
| `constraints.md` | 制約・前提条件 | 各種 |

※ 詳細は `docs/design/artifacts.md` を参照

## 完了条件

- [ ] output.md が作成されている
- [ ] 次SubStageのインプットが明確

## 次のSubStage

→ `substage-{{N+1}}-{{next-name}}/`
