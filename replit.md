# gameheaven Reviews

An after-purchase feedback site where gameheaven customers rate their experience and the store owner reviews incoming feedback.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/gaming-store-reviews` — customer review flow at `/` and store overview at `/dashboard`
- `artifacts/api-server/src/routes/reviews.ts` — review submission, listing, and summary endpoints
- `lib/db/src/schema/reviews.ts` — PostgreSQL review table and insert model
- `lib/api-spec/openapi.yaml` — source of truth for review API contracts
- `artifacts/gaming-store-reviews/src/index.css` — product theme and responsive styles

## Architecture decisions

- Reviews are stored in the shared PostgreSQL database so submissions persist across refreshes and sessions.
- The customer flow is intentionally login-free to keep the post-purchase rating action quick.
- The owner dashboard is view-only in this first version; authentication can be added before sharing it broadly.
- OpenAPI generation is pinned to Zod 3 output because the workspace currently uses Zod 3.

## Product

- Customers select a 1–5 star rating and can add their name, order reference, and written feedback.
- The home page shows recent feedback and a clear success confirmation after submission.
- The dashboard shows average rating, total reviews, rating distribution, and filterable feedback.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

_Populate as you build — sharp edges, "always run X before Y" rules._

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
