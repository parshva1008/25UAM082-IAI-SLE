# Maze Navigation: BFS vs DFS Profiling

Profiling comparison of **Breadth-First Search (BFS)** and **depth-limited Depth-First Search (DFS)** on a maze-navigation problem (find a path from start to end in a maze graph).

> **Course:** 02AML204 – Introduction to Artificial Intelligence (SLE-2: Profiling Report)
> **Author:** Parshva Sachin Bhabire · PRN 25UAM082 · Division B

## Overview

Both algorithms search the same maze graph and stop when they reach the goal, returning `(path_length, nodes_visited, path)` so they can be compared fairly. The project measures:

- **Execution time** (`time.perf_counter`, 5 runs per algorithm per test case)
- **Nodes visited** (counted inside each function)
- **Path optimality** (shortest path vs. any path)
- **Hot spots** (flame graph of where time is spent)

## Key Results

| Test case | Algo | Avg time (ms) | Nodes visited | Path length |
|---|---|---|---|---|
| Best (2-step maze) | BFS | 0.0088 | 2 | 1 |
| Best (2-step maze) | DFS | 0.0148 | 5 | 4 |
| Average (5-step maze) | BFS | 0.1763 | 56 | 3 |
| Average (5-step maze) | DFS | 0.0182 | 6 | 5 |
| Worst (10×10 maze) | BFS | 4.2386 | 1,123 | 5 |
| Worst (10×10 maze) | DFS | 0.0328 | 8 | 7 |

**Takeaways**

- BFS always found the **shortest** path; DFS never did (up to 4 moves longer).
- DFS visited far fewer nodes and ran faster here, but only because its fixed direction order happened to suit these mazes. That is a property of the layout, not a general advantage.
- In the profile, `bfs_shortest_path()` took ~96% of runtime (~630 of ~656 ms); `dfs_shortest_path()` took under 2%.
- BFS needs O(b^d) memory, so it will struggle on much larger grids. DFS needs only O(m), but needs a heuristic (e.g. A\* with Manhattan distance) to find optimal paths.

## Project Structure

> Adjust to match your actual files.

```
.
├── maze_search.py          # get_neighbors, mark_visited, check_goal, bfs_shortest_path, dfs_shortest_path
├── run_experiments.py      # driver: runs all test cases, writes results.json
├── make_charts.py          # generates Fig. 1 (maze/path) and Fig. 3 (timing chart)
├── results.json            # raw timing / node-count results
├── flamegraph.svg          # profiling output (Fig. 2)
├── report/
│   └── SLE2_25UAM082.docx  # full profiling report
├── README.md
└── CONTRIBUTING.md
```

## Requirements

- Python 3.9+
- `matplotlib` (for charts)
- [`py-spy`](https://github.com/benfred/py-spy) (optional, for the flame graph)

```bash
pip install matplotlib py-spy
```

## Usage

Run the experiments (5 runs per algorithm per test case):

```bash
python run_experiments.py
```

Generate the flame graph:

```bash
py-spy record -o flamegraph.svg --rate 100 -- python run_experiments.py
```

If `py-spy` can't be installed (e.g. sandboxed or offline machines), `cProfile` gives an equivalent view:

```bash
python -m cProfile -o profile.out run_experiments.py
```

## Methodology Notes

- **Timing** uses `time.perf_counter()`, since sampling profilers are too coarse for very fast calls.
- **Flame graph** shows where time is spent; the original report used `cProfile` in place of `py-spy` because of an offline environment.
- **Nodes visited** = positions taken from the frontier (queue for BFS, stack for DFS).
- **Test mazes:** a 2-step maze (best), a 5-step maze (average) and a 10×10 maze (worst).

## AI Disclosure

Claude (Anthropic) assisted with the BFS/DFS code, profiling and chart scripts, and report drafting. The author chose the test mazes, ran the experiments, checked the results and wrote the analysis and conclusions.

## License

Add a license of your choice (e.g. MIT) before publishing.
