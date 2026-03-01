# AI Pathfinder — Informed Search with Dynamic Obstacles

A grid-based pathfinding visualizer built with Python and Tkinter. Implements **Greedy Best-First Search** and **A\*** with **Manhattan** and **Euclidean** heuristics, plus a **Dynamic Mode** that spawns obstacles in real-time and replans the path automatically.

---

## Requirements

| Requirement | Version |
|---|---|
| Python | 3.7 or higher |
| Tkinter | Included with Python (no install needed) |

> **Tkinter** is part of Python's standard library. No `pip install` is required for this project.

---

## How to Check if Python is Installed

Open a terminal (Command Prompt on Windows, Terminal on macOS/Linux) and run:

```bash
python --version
```

or

```bash
python3 --version
```

You should see something like `Python 3.10.5`. If Python is not installed, download it from [https://www.python.org/downloads/](https://www.python.org/downloads/).

---

## How to Run

### Step 1 — Download the file

Save `ai_pathfinder.py` to any folder on your computer, for example:

```
C:\Users\YourName\Desktop\ai_pathfinder\
```

### Step 2 — Open a terminal in that folder

**Windows:**
- Open Command Prompt
- Type `cd Desktop\ai_pathfinder` and press Enter

**macOS / Linux:**
- Open Terminal
- Type `cd ~/Desktop/ai_pathfinder` and press Enter

### Step 3 — Run the program

```bash
python ai_pathfinder.py
```

or (on some systems):

```bash
python3 ai_pathfinder.py
```

The GUI window will open immediately.

---

## Tkinter Not Found? (Linux only)

On some Linux distributions Tkinter is not bundled with Python. Install it with:

**Ubuntu / Debian:**
```bash
sudo apt-get install python3-tk
```

**Fedora / RHEL:**
```bash
sudo dnf install python3-tkinter
```

**Arch Linux:**
```bash
sudo pacman -S tk
```

macOS and Windows users do **not** need this step.

---

## How to Use the Application

### 1. Set Up the Grid

| Button | What it does |
|---|---|
| **Set Start Node** | Click this, then click any cell to place the start (purple) |
| **Set Target Node** | Click this, then click any cell to place the target (dark blue) |
| **Place/Remove Wall** | Click or drag on cells to toggle walls (black) |
| **Clear Grid** | Resets the entire grid |

### 2. Resize the Grid (Optional)

- Enter desired **Rows** and **Cols** values in the spinboxes (5–25)
- Click **Apply Grid Size**
- Cell size auto-adjusts so the grid always fits the window

### 3. Generate a Random Map (Optional)

- Adjust the **Density** slider (0.10 = 10% walls, 0.60 = 60% walls)
- Click **Generate Random Map**
- Start and Target nodes are cleared — place them again after generating

### 4. Choose Algorithm and Heuristic

**Algorithm dropdown:**
- `Greedy Best-First` — uses only `f(n) = h(n)`, fast but not always optimal
- `A*` — uses `f(n) = g(n) + h(n)`, always finds the shortest path

**Heuristic dropdown:**
- `Manhattan` — best for grids without diagonal movement `|Δrow| + |Δcol|`
- `Euclidean` — straight-line distance `√(Δrow² + Δcol²)`

### 5. Run the Search

- Click **▶ Start Search**
- Watch the visualization:
  - 🟡 **Yellow** = Frontier nodes (in priority queue, not yet expanded)
  - 🔵 **Light Blue** = Explored/visited nodes (number = visit order)
  - 🟢 **Green** = Final path found
- Click **■ Stop Search** to interrupt at any time

### 6. Dynamic Mode

- Check **Enable Dynamic Obstacles**
- Adjust **Spawn Prob** slider (e.g. `0.10` = 10% chance per step)
- Click **▶ Start Search**

What happens:
1. The initial path is computed and shown with animation
2. An 🔴 orange-red circle (the agent) moves step by step along the path
3. At every step, a new obstacle may spawn randomly on the grid
4. If the obstacle lands **on the current path**, the agent immediately replans from its current position
5. If the obstacle is **off the path**, the agent continues without any recalculation (efficient)

---

## Metrics (shown at the bottom)

| Metric | Description |
|---|---|
| **Nodes Visited** | Total number of nodes expanded during search |
| **Path Cost** | Number of steps in the final path |
| **Exec Time** | Total time taken to find the path (milliseconds) |

---

## Color Legend

| Color | Meaning |
|---|---|
| 🟣 Purple | Start node |
| 🔵 Dark Blue | Target node |
| ⬛ Black | Wall / obstacle |
| 🟡 Yellow | Frontier (open list) |
| 🔵 Light Blue | Visited / explored |
| 🟢 Green | Final path |
| 🔴 Orange-Red circle | Agent (Dynamic Mode only) |

---

## Project Structure

```
ai_pathfinder/
│
├── ai_pathfinder.py      # Main application (single file, no dependencies)
└── README.md             # This file
```

---

## Algorithm Summary

### Greedy Best-First Search
- **Formula:** `f(n) = h(n)`
- Only considers estimated distance to target
- Fast, explores fewer nodes
- Does **not** guarantee the shortest path

### A* Search
- **Formula:** `f(n) = g(n) + h(n)`
- `g(n)` = actual cost from start to current node
- `h(n)` = heuristic estimate from current node to target
- Guarantees the **optimal (shortest) path**
- Explores more nodes than GBFS but produces better results

---

## Tested On

- Windows 10 / 11 — Python 3.9, 3.10, 3.11
- Ubuntu 22.04 — Python 3.10 with `python3-tk`
- macOS Ventura — Python 3.11
