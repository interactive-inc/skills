---
name: software-stack-tanstack
description: "?"
user-invocable: false
disable-model-invocation: false
metadata:
  author: shigurenimo
  description: TanStack（Router/Query/Form/Table）と Hono API + Drizzle で型安全な React アプリを構築する。
  dev: true
---

# TanStack App

TanStack Start (React) + TanStack Query + Hono + Drizzle.

## Patterns

- hc client で型安全 API 呼び出し
- 更新は refetch（`invalidateQueries` 使わない）
- Suspense + `use()` でデータ取得
- Skeleton で loading
- query は子に渡す

## References

- [Hono API](references/hono-api.md)
- [hc client](references/hc-client.md)
- [Auth](references/auth.md): JWT + Cookie、authMiddleware
- [Session](references/session-context.md): React Context + Query、useSession
- [Suspense + use()](references/suspense-use.md)
- [Cloudflare](references/cloudflare.md): Workers + D1、HonoEnv、databaseMiddleware
- [TanStack Start BASIC auth](references/tanstack-start/basic-auth.md)

## Claude Tools

横断ツールは software-stack を参照。

### shadcn/ui

`components.json` 利用時。`npx skills add shadcn/ui`。

### react-best-practices

`npx skills add vercel-labs/agent-skills --skill react-best-practices`。

### next-best-practices

Next.js 利用時。`npx skills add vercel-labs/next-skills --skill next-best-practices`。Optional: `--skill next-upgrade`、`--skill next-cache-components`。

### stitch-skills

DESIGN.md ＋ shadcn 統合。`stitch-design` / `design-md` / `enhance-prompt` を `--global` で。shadcn 利用時は `shadcn-ui` も。

### taste-design

stitch-skills と併用、premium UI 基準。`.agents/skills/taste-design` を symlink。
