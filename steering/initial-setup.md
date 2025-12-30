# 初回セットアップ（ソクラテス式ヒアリング）

このPowerは不特定多数のプロジェクトでの利用を想定しています。
そのため、`coding-standards.md` / `review-rules.md` は「サンプル」として提供し、初回にプロジェクトに合わせて微調整する前提です。

## 目的

- プロジェクトの前提（言語/フレームワーク/レビュー方式/CI）を明確化する
- `steering/` の内容を「自分たちの運用」に合わせて整える
- `steering/knowledge-workflow.md` の原則を守れるように、行動を促す導線を用意する

## Step 0: 回答を残す（推奨）

以下を作成・更新してください。

- `steering/project-profile.md`

このファイルは「初回の回答の置き場所」です。チームで合意した内容をここに残してください。

## Step 1: ソクラテス式質問（YES/NOで答えたあと、理由を一言で）

### A. プロジェクトの前提

1. このプロジェクトの主要言語は何ですか？（TypeScript / Go / Python / Java / その他）
2. 主なフレームワークは何ですか？（Next.js / React / Spring / FastAPI / その他）
3. コードフォーマッタは何を使いますか？（Prettier / gofmt / black / なし）
4. Linter は何を使いますか？（ESLint / golangci-lint / ruff / なし）
5. テストは何を回しますか？（unit / integration / e2e / なし）

### B. レビュー方式（不特定多数向けにここを最優先で確認）

1. PRベースですか？それともペアプロ/モブ/直push運用ですか？
2. PRベースの場合、レビュー必須人数は何人ですか？（0/1/2+）
3. PRテンプレやチェックリストは運用していますか？
4. 指摘を「ルール化」して自動検知したいですか？（したい/まずはしない）

### C. ナレッジ運用（チューターとしての促し）

1. 「解決したらすぐ書く」を徹底したいですか？（したい/できる範囲で）
2. ドキュメント更新をPRのDefinition of Doneに入れたいですか？
3. 週次振り返りをやりたいですか？（毎週15分）

## Step 2: 回答を反映する場所（どこを直せば良いか）

- `steering/coding-standards.md`
  - 言語/フレームワークに依存する規約（例: React Hooks）を、自分たちの前提に合わせて追加/削除
- `steering/review-rules.md`
  - 使っている言語/静的解析ツールで検出できる粒度に調整
  - PRを使わない運用の場合は「レビュー指摘」ではなく「振り返りで出た改善」などに読み替え
- `steering/knowledge-workflow.md`
  - 運用できる頻度（毎回/週次/リリース前）に合わせて、現実的なトリガーに調整

## Step 3: チューター（行動を促す）運用案

- PRベースの場合:
  - PR作成前に `docs/reviews/tags/` を確認する（既知の指摘を先に潰す）
  - PRに「docs更新チェック」を入れる（troubleshooting / patterns / features の更新）
- PRを使わない場合:
  - 週次/隔週で「変更点と学び」を `docs/learning/` に残す
  - チームの改善点を `docs/patterns/` として残す

## Kiroへの指示（初回にやってほしいこと）

新規プロジェクトでこのPowerを導入した直後、以下を促してください。

1. `steering/project-profile.md` を作成/更新する
2. `steering/initial-setup.md` の質問に答える
3. 回答に合わせて `steering/coding-standards.md` / `steering/review-rules.md` を調整する
