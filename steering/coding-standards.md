# コーディング規約

## 命名規則

### Boolean
- ❌ NG: `const open = true`
- ✅ OK: `const isOpen = true`
- プレフィックス: `is`, `has`, `can`, `should`

### 関数名
- 動詞で始める: `getUserById`, `createOrder`, `validateInput`
- ❌ NG: `userData()` → ✅ OK: `fetchUserData()`

### 定数
- UPPER_SNAKE_CASE: `MAX_RETRY_COUNT`, `API_BASE_URL`

### ファイル名
- コンポーネント: PascalCase (`UserProfile.tsx`)
- ユーティリティ: camelCase (`formatDate.ts`)
- 設定ファイル: kebab-case (`api-config.ts`)

## エラーハンドリング

### 基本ルール
```typescript
// ❌ NG: 空のcatch
try {
  await fetchData();
} catch (e) {}

// ✅ OK: 最低限のログ出力
try {
  await fetchData();
} catch (error) {
  console.error('Failed to fetch data:', error);
  throw error; // または適切なエラーハンドリング
}
```

### ユーザー向けエラー
- 技術的なエラーメッセージをそのまま表示しない
- 日本語で分かりやすいメッセージに変換

## コメント

### JSDoc
- 公開関数には必ずJSDocを書く
- `@param`, `@returns`, `@throws` を明記

### インラインコメント
- 「なぜ」を書く（「何を」はコードを読めば分かる）
- TODO/FIXME には Issue 番号を付ける: `// TODO(#123): 後で修正`

## インポート順序

1. 外部ライブラリ
2. 内部モジュール（絶対パス）
3. 相対パス
4. 型定義

```typescript
// 1. 外部
import { useState } from 'react';
import axios from 'axios';

// 2. 内部（絶対パス）
import { api } from '@/lib/api';
import { Button } from '@/components/ui';

// 3. 相対パス
import { helpers } from './helpers';

// 4. 型
import type { User } from '@/types';
```
