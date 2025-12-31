# QuickStart

SuperKiroを5分で始めるためのガイドです。

## 1. インストール

### Kiro IDE（推奨）

1. Kiro IDEで `Manage Powers` を開く
2. `Add power from GitHub` をクリック
3. リポジトリURLを入力

### 手動インストール

```bash
git clone https://github.com/YOUR_USERNAME/SuperKiro.git
cd SuperKiro

# プロジェクトにコピー
cp -r steering/* YOUR_PROJECT/.kiro/steering/
cp -r hooks/* YOUR_PROJECT/.kiro/hooks/
cp -r docs/* YOUR_PROJECT/docs/
```

## 2. 初回設定（3ファイルだけ）

以下のファイルをプロジェクトに合わせて編集:

| ファイル | 何を書く？ |
|----------|-----------|
| `steering/project-profile.md` | 言語、フレームワーク、チーム規模 |
| `steering/coding-standards.md` | コーディング規約 |
| `steering/review-rules.md` | レビューで指摘されがちなこと |

**ヒント**: `steering/initial-setup.md` を実行すると、対話形式で設定できます。

## 3. 最初の一歩

### トラブルシューティングを記録する

エラーを解決したら、すぐに記録:

```markdown
# docs/troubleshooting/YYYY-MM-DD-issue-name.md

## 症状
何が起きた？

## 原因
なぜ起きた？

## 解決方法
どう直した？
```

### レビュー指摘を蓄積する

PRで指摘を受けたら:

```markdown
# docs/reviews/tags/category.md

## 指摘名

### 問題のコード
（悪い例）

### 修正後のコード
（良い例）
```

## 4. フェーズ管理を始める（オプション）

大きなプロジェクトの場合:

1. `steering/project-structure.md` で階層構造を確認
2. `steering/current-stage.md` に現在位置を記入
3. `docs/project/phases/` 配下にPhase/Stage/SubStageを作成

テンプレート: `docs/_templates/phase/`

## 次のステップ

- 詳細は [README.md](./README.md)
- よくある質問は [FAQ.md](./FAQ.md)
- カスタマイズは `steering/` 配下のファイルを編集
