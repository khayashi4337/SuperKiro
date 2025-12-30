# 2025-01-15: Prisma接続プール枯渇

> このファイルはサンプルです。実際の使用時は削除またはリネームしてください。

## 症状

開発中に以下のエラーが頻発：
```
PrismaClientKnownRequestError: 
Timed out fetching a new connection from the connection pool.
```

## 原因

Next.jsの開発サーバーでホットリロードが発生するたびに、新しいPrismaClientインスタンスが作成され、接続プールが枯渇した。

## 解決方法

### Before

```typescript
// lib/prisma.ts
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

export default prisma
```

### After

```typescript
// lib/prisma.ts
import { PrismaClient } from '@prisma/client'

const globalForPrisma = globalThis as unknown as {
  prisma: PrismaClient | undefined
}

export const prisma = globalForPrisma.prisma ?? new PrismaClient()

if (process.env.NODE_ENV !== 'production') {
  globalForPrisma.prisma = prisma
}
```

## 学び

- 開発環境でのホットリロードはリソースリークの原因になる
- グローバル変数を使ったシングルトンパターンで回避
- 本番環境では不要（サーバーが再起動しないため）

## 関連

- [Prisma公式: Best practice for instantiating PrismaClient](https://www.prisma.io/docs/guides/database/troubleshooting-orm/help-articles/nextjs-prisma-client-dev-practices)
