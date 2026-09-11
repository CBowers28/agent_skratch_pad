# Project Scope & Architecture — Flow Canvas (working title)

> **Status:** Draft for review (CHR-17). No application code has been written yet.
> This document defines *what we are building and why* before we build it, per the
> ticket's request to "further scope out and define this project and these
> requirements before starting."

## 1. Vision

A TL-draw–style infinite canvas for **designing software systems**. Users drop 2D
blocks onto a pannable/zoomable dashboard and connect them into flows. The
differentiator from tldraw: **every block can carry a scoped, structured
description** — the intent, inputs/outputs, and constraints of that piece of the
system — so engineers can reason about a design, not just sketch it.

Think "tldraw for architecture diagrams, where each box is a documented,
scope-able unit."

## 2. What tldraw gives us for free (and why we build on it)

The foundation decision (see CHR-17 discussion) is to build on the **official
open-source [tldraw](https://tldraw.dev) SDK** rather than a hand-rolled canvas.
It provides, out of the box:

- Infinite, pannable, zoomable canvas with smooth performance.
- Selecting, moving, resizing, rotating shapes.
- Undo/redo, copy/paste, keyboard shortcuts.
- Local persistence and a documented store/state model.
- A **custom shape API** — the extension point we need for scoped flow blocks.

This lets us spend our effort on the *unique* value (scoped descriptions, flow
semantics) instead of re-implementing canvas mechanics.

## 3. Proposed tech stack

| Concern            | Choice                                   | Rationale                                              |
| ------------------ | ---------------------------------------- | ------------------------------------------------------ |
| Language           | TypeScript                               | Type safety for the shape/flow data model.             |
| UI framework       | React                                    | Required by tldraw; large ecosystem.                   |
| Build tool / dev   | Vite                                     | Fast dev server + HMR; simple config.                  |
| Canvas engine      | tldraw SDK                               | See §2.                                                |
| Package manager    | npm (pnpm optional)                      | Default; low friction.                                 |
| Lint / format      | ESLint + Prettier                        | Consistent, clean code (ticket asks for this).         |
| IDE                | WebStorm                                 | Requested; works natively with Vite/React/TS.          |

WebStorm note: a Vite + React + TS project *is* a standard WebStorm/JetBrains web
project. No special setup beyond opening the folder; run configs can be committed
later if desired.

## 4. Milestones

Each milestone is intended to map to one ticket so scope stays reviewable.

- **M0 — Scoping (this ticket, CHR-17):** Define vision, requirements, stack,
  architecture. Add README (living docs), gitignored agent guidance file, and
  `.gitignore`. **No app code.**
- **M1 — Environment + basic canvas:** Scaffold Vite + React + TS on tldraw.
  Working infinite canvas: pan, zoom, add/move/delete default shapes and 2D
  images. Lint/format wired up. This satisfies the ticket's core "environment
  that allows for boxes to be drawn."
- **M2 — Custom "flow block" shape:** A first-class block type that renders on the
  canvas and stores a title + scoped description.
- **M3 — Scoped descriptions:** Rich, structured description panel per block
  (intent, inputs, outputs, constraints). The core differentiator.
- **M4 — Flow connections:** Typed arrows/edges between blocks with their own
  metadata.
- **M5 — Persistence & sharing:** Durable save/load; export/import of a design.

## 5. Requirements for M1 (the buildable next step)

**Functional**
- Open the app in a browser and see a full-window infinite canvas.
- Pan (drag/scroll) and zoom (wheel/pinch/controls).
- Add a rectangle/box; move, resize, and delete it.
- Place a 2D image on the canvas and move it (parity with tldraw dashboards).
- State persists across reloads (tldraw local persistence).

**Non-functional**
- Clean, documented code; ESLint + Prettier pass with no errors.
- Clear project structure (see §6) so future shapes slot in predictably.
- README kept current as living documentation (ticket requirement).

## 6. Proposed project structure (for M1)

```
/                     repo root
├── README.md         living documentation (overview, how to run, status)
├── docs/
│   └── SCOPE.md       this document
├── AGENTS.md          agent guidance (gitignored, local-only)
├── .gitignore
├── index.html         Vite entry
├── package.json
├── tsconfig.json
├── vite.config.ts
└── src/
    ├── main.tsx       React root
    ├── App.tsx        mounts the canvas
    ├── canvas/        tldraw setup + configuration
    ├── shapes/        custom shapes (flow blocks) — added in M2+
    └── styles/        global styles
```

## 7. Open questions

1. **Persistence scope:** Is local-only (browser) fine through M4, with a backend
   deferred to M5? (Assumed yes.)
2. **Collaboration:** Is real-time multiplayer in scope eventually, or single-user
   only? (Affects backend choices; assumed out of scope for now.)
3. **Design/branding:** Any naming or visual direction for the product, or keep the
   "Flow Canvas" working title?
4. **Image hosting:** Should images be embedded (data URLs / local) or uploaded to
   storage? (Assumed embedded/local for M1.)

## 8. Decisions log

- **2026-09-10:** Build on the tldraw SDK (Vite + React + TS), not a custom canvas.
  Chosen for speed and extensibility toward scoped flow blocks. (CHR-17)
- **2026-09-10:** Deliver M0 as docs-only for review before writing app code, per
  ticket instruction to scope first. (CHR-17)
