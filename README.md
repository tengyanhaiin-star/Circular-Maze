# ⭕ Circular Maze

A procedurally generated polar-coordinate maze playable in any modern browser — no installation required. Works on both desktop and iPhone.

---

## How to Play

Navigate a glowing ball from the **center hub** to the **exit gap** on the outermost ring.

| Control | Keyboard | D-pad |
|---|---|---|
| Move outward | ↑ | ↑ |
| Move inward | ↓ | ↓ |
| Rotate counter-clockwise | ← | ← |
| Rotate clockwise | → | → |

On mobile, use the on-screen D-pad. On desktop, arrow keys work directly after clicking the maze.

---

## Difficulty Modes

| Mode | Description |
|---|---|
| 🗺️ **Treasure Hunt** (Easy) | The full maze is visible at all times. |
| 🏝️ **Island Survival** (Medium) | Fog of war — only your current cell and directly reachable neighbors are visible. Cells you have already visited remain permanently revealed. |
| 🕳️ **Cave Explorer** (Hard) | Permanent darkness — only your current cell and directly reachable neighbors are ever visible, even after backtracking. |

In all fog modes, the solution path and trail are also hidden in obscured areas.

---

## Maze Generation

The maze is built using a **recursive backtracker** (depth-first search with backtracking), which guarantees:

- Every cell is reachable — the maze is always solvable.
- There is exactly one path between any two cells (a perfect maze).

The grid uses **polar coordinates**: concentric rings divided into equal sectors. Every ring has the same number of sectors, so each cell has a unique inner and outer neighbor with no branching ambiguity.

Ring widths follow a **non-linear distribution** (radius ∝ r^0.7), giving inner rings more radial space so the maze looks balanced rather than cramped at the center.

---

## Settings

Open the settings drawer with the ⚙️ button (top right).

| Setting | Description |
|---|---|
| **Seed** | Integer seed for the PRNG. The same seed always produces the same maze. Use Previous / Next to step through seeds, or randomize. |
| **Rings** | Number of concentric rings (3–24). More rings = larger, harder maze. |
| **Sectors** | Number of angular divisions per ring (4–30, even numbers). More sectors = denser maze. |
| **Show Solution** | Highlights the shortest path from center to exit (BFS). Hidden in fogged areas. |
| **Show Trail** | Draws a line through every cell you have visited, in order. Hidden in fogged areas. |

---

## Technical Details

- **Single HTML file** — no build tools, no dependencies beyond p5.js (loaded from CDN).
- **PRNG** — Mulberry32, seeded for fully reproducible mazes.
- **Pathfinding** — BFS from hub entry cell to outermost ring sector 0.
- **Arc rendering** — all arcs are drawn as polylines (`beginShape/vertex`) rather than `p5.arc()`, avoiding fill artifacts.
- **Trail and solution curves** — same-ring segments are drawn as circular arcs at the ring's mid-radius; cross-ring segments are straight radial lines.
- **Mobile** — touch events use `touchstart` + `preventDefault` to avoid double-firing and iOS fullscreen gestures. Layout uses `100dvh` and `safe-area-inset-bottom` for iPhone notch/home-bar compatibility.
- **Font** — [Roboto](https://fonts.google.com/specimen/Roboto) (Google Fonts).

---

## Quickstart

Open the [Circular Maze](https://tengyanhaiin-star.github.io/Circular-Maze/) in any browser, no server needed.

To share a specific maze, note the seed number and send it.

---

## License

MIT — see [LICENSE](LICENSE) for details.
