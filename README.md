# Flow Canvas (working title)

A TL-draw–style infinite canvas for **designing software systems**. Drop 2D blocks
onto a pannable, zoomable dashboard and connect them into flows — but unlike a
plain whiteboard, **every block can carry a scoped, structured description** (its
intent, inputs/outputs, and constraints) so engineers can reason about a design,
not just sketch it.

> This README is **living documentation**. It is kept current as the project
> evolves. For the full plan, see [`docs/SCOPE.md`](docs/SCOPE.md).

## Status

| Milestone | Description                                   | State          |
| --------- | --------------------------------------------- | -------------- |
| M0        | Scoping & docs (this ticket, CHR-17)          | 🟡 In review   |
| M1        | Environment + basic infinite canvas           | ⚪ Not started |
| M2        | Custom "flow block" shape                      | ⚪ Not started |
| M3        | Scoped descriptions per block                  | ⚪ Not started |
| M4        | Flow connections between blocks                | ⚪ Not started |
| M5        | Persistence & sharing                          | ⚪ Not started |

**Right now (M0):** we have defined the vision, tech stack, architecture, and
milestones. No application code has been written yet — that begins at M1 once the
plan is approved.

## Planned tech stack

- **TypeScript + React + [Vite](https://vitejs.dev)**
- **[tldraw](https://tldraw.dev) SDK** for the canvas (pan/zoom/move + custom shapes)
- **ESLint + Prettier** for clean, consistent code
- Developed as a **WebStorm** project

See [`docs/SCOPE.md`](docs/SCOPE.md) §3 for rationale.

## Getting started

> Not applicable yet — there is no app to run during M0. Once M1 lands, this
> section will document `npm install` / `npm run dev` and how to open the project
> in WebStorm.

## Repository layout (planned)

```
├── README.md         you are here — living documentation
├── docs/SCOPE.md      full scope, architecture, milestones, decisions log
├── AGENTS.md          agent/contributor guidance (local-only, gitignored)
└── src/               application code (added at M1)
```

## Contributing / working notes

- One milestone per ticket to keep changes reviewable.
- Update this README and `docs/SCOPE.md` whenever behavior or structure changes.
- See `AGENTS.md` for AI-agent working rules (local-only).
