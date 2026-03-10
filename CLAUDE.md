# War Of Billions — Claude Code Instructions

## Project Overview

War Of Billions is a UI-heavy strategy/action game. This file contains instructions for Claude Code when working in this repository.

## Tech Stack

- **Frontend:** React + TypeScript (no backend — all logic runs client-side)
- **Docs:** Markdown (all documentation must be `.md`)
- **Data:** CSV for balance spreadsheets and translation tables
- **UI Design:** Excalidraw (`.excalidraw` files live in `docs/design/ui/`)

## Repository Layout

| Path               | Purpose                                      |
|--------------------|----------------------------------------------|
| `frontend/`        | React + TypeScript client (the whole game)   |
| `docs/gdd/`        | Game Design Documents and Glossary of Terms  |
| `docs/design/ui/`  | Excalidraw mockups + exported images         |
| `docs/design/systems/` | Game system design docs (.md)           |
| `docs/lore/`       | Story, factions, world-building              |
| `data/balance/`    | Balance spreadsheets (.csv)                  |
| `data/i18n/`       | Translation tables (.csv)                    |

## Conventions

- All documentation must be written in Markdown.
- Balance data lives in `data/balance/` as `.csv` files.
- Translation/localisation tables live in `data/i18n/` as `.csv` files.
- Excalidraw UI mockups (`.excalidraw`) are stored alongside exported `.png` or `.svg` in `docs/design/ui/`.
- Frontend is UI-heavy — prioritise component clarity and typed props.
- No backend. All game state, logic, and procedural generation runs in the browser.

## Notes

- UI design is done on iPad via Excalidraw + Working Copy. Do not move or rename files in `docs/design/ui/` without confirming first.
