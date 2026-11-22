# tulivu-web

Tulivu frontend SPA (React + Vite + Tailwind), deployed as a static site (AWS Amplify).

## Scope
- Frontend UI only (`src/`, `index.html`, Vite build).
- Calls the Tulivu API via `VITE_API_BASE_URL` (defaults/fallback handled in client config as applicable).

## Dev
```bash
pnpm install
VITE_API_BASE_URL=http://127.0.0.1:8787 pnpm dev
```

## Build
```bash
pnpm install --frozen-lockfile
pnpm build
```
Build output: `dist/client` (matches `amplify.yml`).

## Shared packages
`packages/shared` and `packages/ad-platforms` are currently vendored copies from the monorepo split.
Target state (Decision #3): consume `tulivu-packages` via git submodule (pinned ref) or versioned package. Replace vendored copies once wiring is finalized.

## Deploy
- Amplify build spec: `amplify.yml`.
- Set `VITE_API_BASE_URL` per branch/environment in Amplify.
- SPA rewrites to `/index.html` must remain configured in Amplify.
