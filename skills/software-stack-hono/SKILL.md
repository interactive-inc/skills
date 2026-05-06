---
name: software-stack-hono
description: "?"
user-invocable: false
disable-model-invocation: false
metadata:
  author: shigurenimo
  description: Hono フレームワークを用いた TypeScript バックエンド開発スキル。
  dev: true
---

# Hono Backend

Layered (Interface → Application → Infrastructure → Domain). Lib は横断のみ。

## Layout

```
api/
├── domain/
│   ├── entities/
│   ├── values/
│   └── errors/
├── application/
├── infrastructure/
│   ├── repositories/
│   ├── adapters/
│   └── converters/
├── interface/
│   ├── routes/
│   ├── middlewares/
│   ├── serializers/
│   └── factory.ts
├── lib/
├── migrations/
├── drizzle.schema.ts
├── env.d.ts
└── index.ts
```

## Layer Rules

- Interface: validation、auth、HTTPException 変換
- Application (Service): 1 class = 1 use case、`execute()`、throw せず `T | Error` を return
- Domain: Entity / Value Object / business rules、外部依存なし
- Infrastructure: Repository / Adapter で DB ・外部 API を隔離
- Lib: 横断的関心事のみ、外部サービス連携は含めない

## Domain

- Entity は DB を知らない（`fromRecord()` を持たない）。DB → Entity 変換は Repository の責務
- Factory メソッドは具体名（`create()` より `createWithEmail()`）

## Naming

- Entity ⇒ `xxx.entity.ts`
- Value ⇒ `xxx.value.ts`
- Repository ⇒ `xxx.repository.ts`
- Adapter ⇒ `xxx.adapter.ts`
- Use Case ⇒ `動詞-名詞.ts`（`create-customer.ts`、`update-customer.ts`）
- Route ⇒ `resource.$param.ts`（`customers.$customer.ts`）

### Use Case Prefix

`create-` / `update-` / `delete-` / `fetch-` / `get-` / `bulk-` / `sync-` / `upsert-`

### Route File

- `/customers` ⇒ `customers.ts`
- `/customers/:customer` ⇒ `customers.$customer.ts`
- `/customers/:customer/orders` ⇒ `customers.$customer.orders.ts`
- `/customers/search` ⇒ `customers.search.ts`

## References

### Domain

- [Entity](references/domain-entity.md)
- [Value Object](references/domain-value.md)
- [Error](references/domain-error.md)

### Application

- [Service](references/application-service.md)

### Infrastructure

- [Repository](references/infrastructure-repository.md)
- [Adapter](references/infrastructure-adapter.md)

### Interface

- [Route Handler](references/interface-route-handler.md)
- [Entry Point](references/interface-entry-point.md)
- [Error Handling](references/interface-error-handling.md)

### Common

- [Drizzle Schema](references/drizzle-schema.md)
- [Lib](references/lib-structure.md)

## Claude Tools

横断ツールは software-stack を参照。

### hono-skill

`npx skills add yusukebe/hono-skill`。Plugin: `/plugin marketplace add yusukebe/hono-skill` → `/plugin install hono-skill@hono`。

### sentry-for-ai

Sentry 利用時。`npx skills add getsentry/sentry-for-ai`。前提: `sentry-cli`。
