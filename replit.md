# God Grace Boutique

A luxurious African fashion e-commerce website for God Grace Boutique — featuring a full product catalog, shopping cart, WhatsApp ordering, admin dashboard, and PostgreSQL backend.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 8080)
- `pnpm --filter @workspace/god-grace-boutique run dev` — run the frontend (port 18720)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Frontend: React + Vite + Tailwind CSS + Framer Motion
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `lib/api-spec/openapi.yaml` — API contract (source of truth)
- `lib/db/src/schema/` — DB tables (products, categories, testimonials, orders, admins)
- `artifacts/api-server/src/routes/` — Express route handlers
- `artifacts/god-grace-boutique/src/pages/` — React pages
- `artifacts/god-grace-boutique/src/lib/cart-context.tsx` — Cart state (localStorage)

## Admin Access

- URL: `/admin`
- Username: `Busayo30`
- Password: `aliyat71016`

## WhatsApp Ordering

- Number: 0575354633 (formatted as 237575354633 for international wa.me link)
- Cart page generates a pre-filled WhatsApp message with all order details

## Payment Methods Displayed

- Wave — pay to 0575354633
- MTN Mobile Money — pay to 0575354633

## Architecture decisions

- Cart state lives entirely in localStorage + React Context (no backend cart session)
- Admin auth uses a simple token stored in localStorage (suitable for boutique owner use)
- Product prices stored as `numeric` in DB, converted to `number` in API responses
- Orders are created in the backend when user clicks "WhatsApp To Order" for record-keeping

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- After OpenAPI spec changes: run `pnpm --filter @workspace/api-spec run codegen` before touching routes or frontend
- API server must be restarted after route changes (it bundles with esbuild)
- The `sort` query param expects `price_asc`, `price_desc`, or `newest`
