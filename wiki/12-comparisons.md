# Algorithm comparison guide

[Home](../README.md)

**Source basis:** synthesis of the problem-solving and optimization decks, the three readings, and supplied Python code. Recommendations below are study judgments conditional on the modeled problem.

## Contents

- [Search and reasoning](#search-and-reasoning)
- [Optimization](#optimization)
- [Selection examples](#selection-examples)

## Search and reasoning

| Method | Main information | Suitable question | Main risk |
|---|---|---|---|
| BFS | Depth | Find fewest actions with equal costs | Exponential memory |
| DFS | Current branch | Explore with limited traversal memory | Loops, poor path quality |
| Greedy best-first | Estimated distance to goal | Quickly pursue promising states | Ignores paid cost |
| A* | Paid cost plus lower-bound estimate | Find cheapest path | Heuristic conditions and memory |
| Minimax | Opponent-aware utility | Choose a move against optimal opposition | Large game tree |
| Alpha–beta | Minimax bounds | Same evaluated-game decision more efficiently | Poor ordering gives little pruning |
| CSP backtracking | Variables, domains, constraints | Find a valid assignment | Combinatorial combinations |
| Prolog proof search | Relations, rules, unification | Find substitutions satisfying a query | Depth-first loops and procedural effects |

Search finds an action path; minimax finds an opponent-aware strategy; CSP finds a satisfying assignment; Prolog searches for a proof/substitution. They can share implementation ideas without solving identical problems.

## Optimization

| Method | Candidate representation | Maintained information | Main update | Typical fit | Main limitation |
|---|---|---|---|---|---|
| GD | Continuous vector | Current point and gradient | Move downhill | Smooth differentiable objectives | Local minima / step-size sensitivity |
| SA | Candidate with a neighborhood | Current and best, temperature | Random move with probabilistic acceptance | Discrete or continuous rugged objectives | Cooling and proposal design |
| GA | Encoded population | Fitness and genetic material | Selection, crossover, mutation | Mixed or structured spaces | Encoding, diversity, evaluation cost |
| PSO | Real-vector swarm | Velocity and personal/social bests | Momentum and attraction | Continuous derivative-free search | Premature convergence / instability |
| ACO | Constructed feasible solutions | Shared pheromone matrix | Probabilistic construction and reinforcement | Routes and other combinatorial tasks | Stagnation and construction cost |
| ABC | Food-source vectors | Source quality and trial counts | Neighbor comparisons and scout resets | Continuous derivative-free search | Parameter sensitivity / refinement speed |

These “typical fit” entries describe basic versions. Variants can extend them to other spaces. None has a universal empirical advantage.

| Exploration mechanism | Exploitation mechanism |
|---|---|
| SA: accepting worse moves at positive temperature | SA: favoring improvements as cooling proceeds |
| GA: mutation and varied parents | GA: selection and recombination of successful material |
| PSO: random attractions, dispersed positions, momentum | PSO: attraction to personal/social bests |
| ACO: probabilistic choices and reduced old trails | ACO: reinforcement of successful edges |
| ABC: scout replacement and varied neighbors | ABC: employed/onlooker local improvements |

## Selection examples

- Equal-cost maze: BFS provides a shortest-action solution in a finite model.
- Weighted route with a useful admissible heuristic: A*; account for improved paths.
- Deterministic two-player game: minimax with alpha–beta and a depth limit if needed.
- Timetable with hard restrictions: a CSP; add an objective if some feasible timetables are preferred.
- Family relationships: Prolog relations and queries.
- Smooth known quadratic: GD has a direct informative gradient.
- Rugged black-box continuous objective: consider SA, PSO, GA, or ABC and compare evaluation budgets.
- TSP route construction: ACO or a permutation-aware GA; compare with suitable specialized baselines.

An exam explanation should identify representation, available information, constraints, desired guarantee, and resources before naming the algorithm.
