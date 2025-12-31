# SuperKiro 運用オンボーディングガイド

新しくチームに参加したメンバー向けの運用ガイドです。

## なぜナレッジ蓄積が必要なのか

### チームでよくある問題

1. **「前にも同じエラー見たけど、どう解決したっけ...」**
   - 同じ問題を何度も調べ直す時間のムダ

2. **「このコード、なんでこうなってるんだろう」**
   - 意図や経緯がわからない。書いた人に聞くしかない

3. **「PRレビューで同じ指摘を繰り返し受ける」**
   - 過去の指摘が共有されていない

4. **「前任者が退職して、仕様がわからない」**
   - 知識が個人に閉じている

### SuperKiroの解決策

**「解決したらすぐ書く」を仕組みで支援**

- テンプレートがあるので何を書くか迷わない
- Hooksで記録を促してくれる
- 検索可能な形式で蓄積される

## 最初に覚える3つのこと

### 1. エラーを解決したら記録する

```markdown
# docs/troubleshooting/2025-01-15-prisma-connection.md

## 症状
Prisma Client が接続エラーを出す

## 原因
開発サーバーのホットリロードで接続が蓄積

## 解決方法
prisma.ts で singleton パターンを使用
```

**ポイント**: 完璧でなくてOK。「たぶんキャッシュ関連」でも書く価値がある。

### 2. PRを作る前に過去の指摘を確認する

1. `docs/reviews/tags/` を見る
2. `steering/review-rules.md` を確認する
3. 同じ指摘を受けないようにコードをチェック

### 3. レビューで指摘を受けたら記録する

```markdown
# docs/reviews/tags/error-handling.md に追記

## try-catch の空キャッチ
- 指摘: catchブロックが空
- 対策: 最低限 console.error を入れる
```

## 日々の運用フロー

### 開発中

```
1. 作業開始
   ↓
2. エラーが発生 → 解決 → docs/troubleshooting/ に記録
   ↓
3. PR作成前に docs/reviews/tags/ を確認
   ↓
4. PR作成
```

### PR作成時

[member-checklist.md](./docs/_templates/member-checklist.md) を使ってセルフチェック：

- [ ] `docs/reviews/tags/` を確認した
- [ ] エラーを解決した場合は記録した
- [ ] 新しいライブラリを使った場合は記録した

### 週末（金曜日15分）

```
1. 今週解決した問題が記録されているか確認
2. 受けたレビュー指摘を追記
3. docs/learning/weekly-retrospective.md を更新（任意）
```

## ドキュメントの書き方

### 最低限これだけ書けばOK

```markdown
## 症状
何が起きたか（エラーメッセージなど）

## 原因
なぜ起きたか（わからなければ「調査中」でもOK）

## 解決方法
どう直したか（コードの Before/After があればベスト）
```

### 書かなくていいこと

- 長い説明や背景
- 完璧な分析
- キレイな文章

**「書かないよりマシ」が最優先**

### Before/After を書くコツ

```markdown
## 解決方法

### Before
```typescript
// 問題のコード
const data = await fetch(url)
```

### After
```typescript
// 修正後のコード
try {
  const data = await fetch(url)
} catch (error) {
  console.error('Fetch failed:', error)
}
```
```

## よくある質問

### Q: 何を書けばいいかわからない

A: テンプレートを使ってください。

- `docs/_templates/troubleshooting.md` - エラー解決時
- `docs/_templates/review-tag.md` - レビュー指摘
- `docs/_templates/library.md` - ライブラリ使用時

### Q: 書く時間がない

A: 完璧を求めない。3行でもいい。

```markdown
## 症状
API タイムアウト

## 原因
不明。たぶんN+1

## 解決方法
キャッシュ入れたら直った
```

これでも次に同じ問題が起きたとき役立つ。

### Q: 同じような記録がすでにある

A: 追記するか、リンクで参照する。

```markdown
## 関連
- [[troubleshooting/2024-12-01-similar-issue]]
```

### Q: どこに書けばいいかわからない

| 状況 | 書く場所 |
|------|----------|
| エラーを解決した | `docs/troubleshooting/` |
| レビューで指摘を受けた | `docs/reviews/tags/` |
| 新しいライブラリを使った | `docs/libraries/` |
| 再利用できそうなコード | `docs/patterns/` |
| 機能の変更履歴 | `docs/features/{feature}/` |

## 最初の1週間でやること

### Day 1: セットアップ

- [ ] このドキュメントを読む
- [ ] [member-checklist.md](./docs/_templates/member-checklist.md) をブックマーク
- [ ] `docs/` フォルダの構成を確認

### Day 2-3: 最初のドキュメント

- [ ] 何かエラーを解決したら、`docs/troubleshooting/` に1つ書いてみる
- [ ] 書いたらリーダーに見せる（フィードバックをもらう）

### Day 4-5: PRサイクル

- [ ] PR作成前に `docs/reviews/tags/` を確認する習慣をつける
- [ ] レビューで指摘を受けたら `docs/reviews/tags/` に追記

### 週末

- [ ] 今週書いたドキュメントを振り返る
- [ ] 書き忘れがあれば追記

## 困ったときは

1. **テンプレートを見る**: `docs/_templates/`
2. **過去の例を見る**: `docs/troubleshooting/` にある既存の記録
3. **リーダーに聞く**: 最初は一緒に書いてもらってもOK

## 心構え

### やってほしいこと

- **すぐ書く**: 後回しにすると忘れる
- **短くてもいい**: 3行でも価値がある
- **わからなくても書く**: 「調査中」でもOK

### やらなくていいこと

- **完璧を目指す**: 後から修正すればいい
- **長文を書く**: 要点だけでいい
- **全部書く**: 該当するものだけでいい

---

次のステップ: [QuickStart.md](./QuickStart.md) で実際の使い方を確認
