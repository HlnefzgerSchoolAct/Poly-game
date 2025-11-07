# Copilot Instructions for Poly Isles: Tide & Tinker (Static, GitHub Pages only)

You are assisting with a single‑player, low‑poly hex island builder playable in the browser, deployed via GitHub Pages (Deploy from a branch). Priorities:
- Simple rules, composable systems, creative expression.
- All‑static site (no servers); saves in `localStorage`; optional URL/base64 share codes.
- Performance first: Instanced mesh rendering, batched updates.

Key files and structure (target):
```
public/index.html
styles/main.css
styles/ui.css
src/main.js           # init Three.js, scene, camera, raycasting
src/hex/**            # axial hex math, neighbors, ring, range
src/systems/**        # state, placement rules, crafting, tide loop
src/ai/**             # dodo & slime behaviors
src/save/**           # save/load, compression, share codes
src/ui/**             # HUD, hotbar, controls, accessibility
assets/models/**      # minimal low‑poly GLTFs or primitives
assets/audio/**       # optional
docs/**               # contracts, roadmap, deploy docs
```

Acceptance criteria patterns:
- Rendering: draw calls <= 120; smooth camera + input; hex picking and ghost placement.
- Systems: deterministic seed reproduction; valid placement + rotation; salvage refunds; Tide phases and Beacon spawns.
- Save: JSON schema `{version, seed, placements, critters, inventory, score, meta}` with export/import + URL params.
- UI: HUD shows resources and Tide timer; hotbar works with click + number keys; relocate mode with `R`.

Guardrails:
- No backend APIs, no auth, no secret tokens.
- Keep bundles small; prefer ESM, tree‑shake, or CDN for Three.js.
- Keep shaders minimal; no heavy post‑processing.

Preferred PR format:
- Title: `feat(scope): concise summary`
- Body: problem, approach, screenshots/gifs, perf notes, test notes.
- Labels by scope: rendering, systems, ui, ai, build, deployment.

Common commands (if using a bundler):
- `npm run dev` start local server for development only
- `npm run build` produce static output (served by Pages root or /docs)