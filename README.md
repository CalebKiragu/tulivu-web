# tulivu-web

Tulivu frontend SPA (React + Vite + Tailwind), deployed as a static site (AWS Amplify).

## Scope
- Frontend UI only (`src/`, `index.html`, Vite build).
- Calls the Tulivu API via `VITE_API_BASE_URL`.

## Branch / environment mapping
- `main` → production Amplify branch (`https://tulivu.app`) with `VITE_API_BASE_URL=https://api.tulivu.app`
- `dev` → development/staging Amplify branch with `VITE_API_BASE_URL=https://dev-api.tulivu.app` (set in Amplify branch env vars)

## Dev
```bash
pnpm install
cp .env.development.example .env.local # or set VITE_API_BASE_URL
pnpm dev
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

## Deploy (Amplify)
- Build spec: `amplify.yml`.
- Set `VITE_API_BASE_URL` per branch/environment in Amplify Console (do not hardcode dev/prod in repo).
- SPA rewrites to `/index.html` (200) must remain configured in Amplify.
- Recommended: connect this repo to Amplify, enable `main` and `dev` branches, set branch env vars accordingly.
