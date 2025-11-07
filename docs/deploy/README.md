# GitHub Pages — Deploy from a branch (Static only)

Hard constraints
- No servers, no dynamic backends, no auth. This is a static site.
- Deployment must use GitHub Pages “Deploy from a branch”.

Repository setup
1) Add your site files to the repository (e.g., `public/`, `src/`, `styles/`, `assets/`).
2) If using Vite:
   - Set `base` in `vite.config` to `'/REPO-NAME/'` for GitHub Pages.
   - `npm run build` outputs to `dist/`. Either:
     - Copy contents of `dist/` to repo root (committed), or
     - Configure Pages to serve from `/docs` and build into `docs/`.

GitHub Pages configuration
- Go to Settings → Pages:
  - Source: “Deploy from a branch”
  - Branch: `main` (or your chosen branch), Folder: `/` (root) or `/docs`
- Wait for Pages to publish (green check).
- Your site will be at: `https://<USERNAME>.github.io/<REPO-NAME>/`

Static asset guidelines
- Keep everything local under `public/` or `assets/`.
- Use relative paths that respect the `base` path.
- No external dynamic scripts that require servers.

Cache busting
- Use hashed filenames (Vite default) for JS/CSS and static assets.
- HTML should not be cached aggressively (default GitHub Pages settings are fine).

Offline (optional, later)
- Add a Service Worker only for caching static assets.
- Do not perform network requests to external services.
- Provide a toggle/opt‑in if you include SW; ensure safe updates.

Troubleshooting
- 404 on refresh for SPA routes: avoid client‑side routes, or add a 404.html that forwards to index.
- Wrong asset paths: verify `vite.config.base` matches `/<REPO-NAME>/`.
- Mixed content/CORS: host all assets locally; avoid cross‑origin requests.

Example vite.config.ts (snippet)
```ts
import { defineConfig } from 'vite';

export default defineConfig({
  base: '/REPO-NAME/',
  build: {
    outDir: 'docs', // so Pages can serve /docs
    emptyOutDir: true,
  },
});
```