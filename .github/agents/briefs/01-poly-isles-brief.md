# Project brief: Poly Isles — Tide & Tinker (single‑player 3D web builder; HTML/CSS/JS + Three.js)

Objective
- Build a creative, replayable, single‑player hex‑tile island builder that runs entirely as a static website (no backend).
- Inspirations: Minecraft (creative building), Apex (shrinking safe zone), Ark (taming helpers), Stardew (cozy farming/progression).
- Technologies: vanilla ES modules (JavaScript), HTML, CSS. Rendering with Three.js. Seeded worldgen; saves in localStorage.

Core loop (per run: ~5–12 minutes)
1) Explore/forage a small hex‑tile island (seeded).
2) Build and craft: place floors/fences/planters/lanterns/workbench.
3) Tame a couple of critters (e.g., Dodo courier, Slime gatherer) to automate simple tasks.
4) The luminous Tide ring shrinks periodically; salvage and compact your base.
5) Reach Beacons inside the ring for blueprints/rare seeds; re‑center the next shrink.
6) Score “Beauty × Efficiency” for layout harmony, compact loops, and output. Save and share runs via code/URL.

Hard constraints (hosting and architecture)
- No servers, no backend calls, no auth.
- Host as a static site on GitHub Pages with “Deploy from a branch”.
- All persistence via localStorage (optional compressed export/import).
- Optional Service Worker later, but only for offline caching (no network calls).

Technical constraints
- Three.js latest stable, vanilla ESM. Optional: seedrandom, LZ‑string/pako. No heavy physics; use raycast placement.
- File layout (lean variant):
  - public/
    - index.html, icons, robots.txt
  - src/
    - main.js, renderer/, systems/, hex/, ai/, ui/, save/
  - assets/
    - models/ (tiny GLTF optional), audio/ (optional)
  - styles/
    - main.css, ui.css
  - docs/
    - contracts.md, design/* (agents produce area docs)
- Build/dev with Vite. Single entry index.html mounting the canvas.

Minimum content scope (MVP)
- World: Single island hex grid (axial q,r) radius ~20–30; 2–3 simple biomes (beach/grass/rock); resource nodes (wood/stone/fiber); day‑to‑night tint only.
- Player: WASD + mouse look; click to harvest/place; rotate blueprint (Right‑click); hotbar 1–6; Relocate mode (R) to pick up.
- Craftables: floor, fence, planter, water barrel, lantern, workbench, dye vat.
- Helpers: Dodo (courier source↔target), Slime (local gatherer) — one job each; tame by feeding 3–5 times.
- Tide: Shrinks every ~3 minutes across 3–4 phases; tiles outside become “soaked” (degrade); Beacons drop inside with blueprint/seed; next shrink re‑centers near last Beacon.
- Scoring: compactness, adjacency loops (workbench/planter/barrel), color harmony, planter throughput. End of run score + unlock small cosmetics/palettes.
- Persistence: Auto‑save to localStorage; export/import share code (seed + placements + critters + inventory + score), URL param support (?seed=…&load=…).
- UI/HUD: resources, Tide timer, objective hint, hotbar; settings: UI scale, colorblind palette.

Acceptance criteria (MVP)
- New Run → seed prompt → spawn → gather → craft Workbench → place 3 Planters → tame 1 Dodo → survive 2 Tide shrinks → reach 1 Beacon → end with score → auto‑save and reload works.
- Performance: ~60fps desktop 1080p on mid hardware; draw calls <= 120; stable memory over 15 min.
- Deterministic world: same seed → same island/Beacons (within RNG bounds).
- Static site; no network required after load; share code import works.

Shared contracts
- Event bus (documented in /docs/contracts.md) with string event names and payloads.
- Save schema: JSON with semver; migrations if schema bumps.
- Units: meters world, seconds time. Y‑up Three.js default.
- Color palettes and scoring heuristics documented.

Versioning and telemetry
- VITE_PUBLIC_BUILD_VERSION injected; no telemetry by default.

Milestone plan
- M1 Renderer + hex grid + picking + camera + Tide ring visual
- M2 Resources + crafting + placement rules + salvage
- M3 Helpers (Dodo/Slime) + basic behaviors + tame UI
- M4 Scoring + Beacons + daily seed override
- M5 Save/export/import + HUD/UX polish + accessibility
- M6 Perf pass + docs + Pages deployment guide
