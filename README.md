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
git submodule update --init --recursive
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
`packages/` is a git submodule pointing to [`tulivu-packages`](https://github.com/CalebKiragu/tulivu-packages.git) (`shared`, `ad-platforms`). Pin updates by advancing the submodule ref in a PR.

```bash
git submodule update --init --recursive
# to update shared packages:
cd packages && git checkout main && git pull && cd .. && git add packages
```

## Deploy (Amplify)
- Build spec: `amplify.yml`.
- Set `VITE_API_BASE_URL` per branch/environment in Amplify Console (do not hardcode dev/prod in repo).
- SPA rewrites to `/index.html` (200) must remain configured in Amplify.
- Recommended: connect this repo to Amplify, enable `main` and `dev` branches, set branch env vars accordingly.
