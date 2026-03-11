# UI Specification

This document defines every screen in the game, how they connect, and what data each one needs from the simulation. It is the contract between the Excalidraw mockups and the React components that will implement them.

**How to use this doc:** For each screen, fill in the sections below after completing its Excalidraw wireframe. The wireframe shows layout and visual hierarchy; this doc captures the data requirements and interaction rules that the wireframe alone cannot express.

See [ExcalidrawTasks.md](ExcalidrawTasks.md) for the wireframe checklist.

---

## Screen Inventory

List every screen here as it is designed. Each entry links to its full section below.

| Screen | Status | Wireframe |
| --- | --- | --- |
| Home System View | Not started | — |
| Galaxy Map | Not started | — |
| Diplomacy Screen | Not started | — |
| Research Allocation | Not started | — |
| Remote System Panel | Not started | — |
| Expansion Launch Screen | Not started | — |
| CDL Suspension Setup | Not started | — |

---

## Navigation Flow

*Describe how the player moves between screens. Which screens are always accessible? Which are contextual (e.g., Remote System Panel only opens from Galaxy Map)? Are any screens modal or overlay?*

---

## Screen Definitions

For each screen, copy this template and fill it in:

### [Screen Name]

**Purpose:** *One sentence — what decision does the player make here?*

**Entry points:** *How does the player reach this screen?*

**Exit points:** *Where can the player go from here?*

**Data required from simulation:**
- *List every piece of state this screen reads. Be specific: not "resources" but "basic_matter_stockpile, exotic_matter_stockpile, compute_generation_rate, waste_rate"*

**Player actions available:**
- *List every action the player can take on this screen and what simulation state it modifies*

**Update frequency:** *Does this screen need to re-render every tick, or only on specific events?*

**Wireframe:** *Link to the .excalidraw file and exported .png once created*

**Notes:** *Open questions, edge cases, anything unresolved*

---

## Shared UI Elements

*Document any UI components that appear on multiple screens (e.g., resource bar, Threat Level indicator, transmission notification). Define them once here so screen definitions can reference them without repeating.*
