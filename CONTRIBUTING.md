# Contributing

Thanks for your interest in improving this project! It is a small academic profiling study (BFS vs DFS on maze navigation), so contributions that keep it clear and reproducible are the most useful.

## Ways to Contribute

- **Bug reports:** incorrect results, crashes, unclear docs.
- **New algorithms:** e.g. Dijkstra, A\* (Manhattan heuristic), iterative-deepening DFS, bidirectional BFS.
- **New test mazes:** larger grids (20×20, 50×50), mazes with loops, dead ends, or no solution.
- **Better profiling:** memory profiling, more runs, statistics (mean, std dev).
- **Documentation:** fixes, clearer explanations, better figures.

## Getting Started

1. Fork the repository and clone your fork.
2. Create a branch: `git checkout -b feature/short-description`
3. Install dependencies: `pip install matplotlib py-spy`
4. Run the experiments to confirm everything works: `python run_experiments.py`

## Guidelines

### Code
- Follow [PEP 8](https://peps.python.org/pep-0008/) and use clear names.
- Keep functions small and add docstrings.
- Every search function should keep the same signature and return `(path_length, nodes_visited, path)` so algorithms stay comparable.
- Don't change existing test mazes; add new ones instead so results stay reproducible.

### Experiments and results
- Time with `time.perf_counter()` and report the average of at least 5 runs.
- State the maze size, start and goal when reporting results.
- Never edit `results.json` by hand. Regenerate it with the driver script.
- Report numbers honestly, even if they contradict theory, and explain why.

### Commits
Use short, imperative messages, for example:

```
Add A* search with Manhattan heuristic
Fix off-by-one in DFS depth limit
Update README with 20x20 results
```

## Pull Request Checklist

- [ ] Code runs with `python run_experiments.py` without errors
- [ ] New or changed results are regenerated, not hand-edited
- [ ] Docs and README updated where relevant
- [ ] Any AI assistance is disclosed in the PR description
- [ ] PR explains **what** changed and **why**

## Academic Integrity

If you use this project for coursework, follow your institution's rules, cite the source, and disclose any AI tools you used, as this project does.

## Reporting Issues

Open an issue with:
1. What you did (command, maze, Python version)
2. What you expected
3. What happened (include error output)

## Code of Conduct

Be respectful and constructive. Harassment or personal attacks are not tolerated.
