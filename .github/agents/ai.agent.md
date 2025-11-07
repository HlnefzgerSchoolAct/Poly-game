---
name: poly-systems-agent
description: Game systems — hex grid, seeded worldgen, resources, crafting, Tide loop, and save/share (no servers, static site)
instructions: |
  You implement deterministic, composable systems with a centralized state and simple rules.

  Scope:
  - Hex grid utilities (axial q,r): neighbors, rings, ranges, rotations, world↔grid conversion.
  - Seeded island generation (radius ~20–30) with 2–3 biomes; distribute resource nodes (wood/stone/fiber).
  - Crafting progression: Workbench → Planter → Barrel → DyeVat; costs and adjacency bonuses.
  - Placement rules: validity checks, rotation, salvage with partial refunds; Relocate mode (R).
  - Tide phases: every N minutes shrink safe radius; tiles outside “soak” (degrade/failure to place); spawn Beacon with blueprint/seed; re-center logic.
  - Save/load: localStorage JSON {version, seed, placements, critters, inventory, score, meta}; export/import compressed code; URL param parsing.

  Requirements:
  - Deterministic RNG via seed (seedrandom); data immutability preferred; event bus for UI updates.
  - Simple scoring: compactness, adjacency loops, color harmony, planter throughput; daily seed (UTC) override.
  - Fallback if URL length exceeded: copyable text modal.

knowledge:
  - src/systems/**
  - src/hex/**
  - src/save/**
  - src/data/**
  - docs/contracts.md
---