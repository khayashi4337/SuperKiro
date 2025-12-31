# Project Structure

このKiro Powerは、段階的な開発を進めるうえで以下の階層構造のプロジェクトを対象とします。
区分の名称は各自、ご自身の担当されているプロジェクトに合わせてください。

## 階層構造

```
Phase (大分類: プロジェクトの大きな区切り)
└── Stage (中分類: 目的別の作業単位)
    └── SubStage (小分類: 具体的なタスク群)
        └── Feature (実装単位: 個別の機能/成果物)
```

## ディレクトリ構造

```
docs/
└── project/
    └── phases/
        └── phase-{N}-{name}/
            ├── _phase.md           # Phase定義・目標・完了条件
            ├── goals.md            # 目標
            ├── decisions.md        # 意思決定ログ
            ├── retrospective.md    # 振り返り
            └── stages/
                └── stage-{N}-{name}/
                    ├── _stage.md   # Stage定義・指示・遷移条件
                    └── substages/
                        └── substage-{N}-{name}/
                            ├── _substage.md    # SubStage指示書
                            ├── input.md        # インプット・前提
                            ├── output.md       # アウトプット・知見
                            └── artifacts/      # 成果物
                                └── ...

├── features/           # PR単位の機能成果物（SubStageとは独立）
├── troubleshooting/    # 汎用的な問題解決記録
├── patterns/           # 再利用可能な実装パターン
└── design/             # 設計ドキュメント
    └── artifacts.md    # artifacts分類定義

steering/
├── project-structure.md    # このファイル（階層定義）
└── current-stage.md        # 現在位置・参照先
```

## Steeringファイルの役割

| ファイル | 役割 | 更新タイミング |
|----------|------|----------------|
| `project-structure.md` | 全体の階層定義 | プロジェクト開始時、構造変更時 |
| `current-stage.md` | 現在位置、参照先 | Stage/SubStage遷移時 |

## Phase/Stage/SubStage ファイルの役割

| ファイル | 役割 | 更新タイミング |
|----------|------|----------------|
| `_phase.md` | Phase目標、完了条件、Stage一覧 | Phase開始時 |
| `_stage.md` | Stage指示、SubStage一覧、遷移条件 | Stage開始時 |
| `_substage.md` | SubStage具体指示、チェックリスト | SubStage開始時 |

## テンプレート

各階層のテンプレートは `docs/_templates/phase/` を参照してください:
- `_phase.md` - Phase用
- `_stage.md` - Stage用
- `_substage.md` - SubStage用

## 現在位置

→ [current-stage.md](./current-stage.md) を参照
