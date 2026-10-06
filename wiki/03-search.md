# Problem formulation and search

[Home](../README.md) · [Next: games](04-games.md)

**Course source:** `02_Problem Solving.pptx`, slides 2–16, including image-only algorithm traces and heuristic definitions.

## Contents

- [Formulating a problem](#formulating-a-problem)
- [Graphs, trees, and repeated states](#graphs-trees-and-repeated-states)
- [Search strategies](#search-strategies)
- [Heuristics and A-star guarantees](#heuristics-and-a-star-guarantees)
- [Worked search example](#worked-search-example)
- [A-star pseudocode](#a-star-pseudocode)

## Formulating a problem

A problem-solving agent formulates a problem, finds an action sequence, and executes it. The lecture's basic planning model assumes an observable, deterministic, discrete, static environment.

| Component | Meaning | Route example |
|---|---|---|
| Initial state | Starting situation | Arad |
| Actions | Available choices in a state | Drive to an adjacent city |
| Transition model | Result of an action | `Result(Arad, drive_to_Sibiu)=Sibiu` |
| Goal test | Condition for completion | Current city is Bucharest |
| Cost | Numerical price of actions/path | Total kilometers |

The **state space** contains states reachable under the transition model. A solution is a sequence of actions from start to a goal. An optimal solution minimizes total path cost under the selected cost definition.

## Graphs, trees, and repeated states

A state graph describes the problem. A search tree describes paths explored by an algorithm: the same state can occur in multiple tree nodes with different parents and costs.

The **frontier** holds generated nodes awaiting expansion. An **explored/closed set** records expanded states. Repeated-state detection prevents cycles, but “never revisit a state” is not universally correct for cost-sensitive search: discovering a cheaper route may require updating or reopening it.

**Study supplement:** a search node usually stores the state, parent, action, and accumulated cost. This permits reconstructing the final action sequence.

## Search strategies

Let $b$ be the branching factor, $d$ the shallowest goal depth, and $m$ the maximum depth searched.

| Algorithm | Frontier ordering | Complete? | Optimal? | Typical tree-search time / space |
|---|---|---|---|---|
| BFS | FIFO, shallowest first | Yes for finite branching and finite-depth goal | Yes with equal positive step costs | Exponential in $d$ / exponential in $d$ |
| DFS | LIFO, deepest first | Finite graph with duplicate control; not arbitrary infinite trees | No | $O(b^m)$ / $O(bm)$ |
| Greedy best-first | Lowest $h(n)$ | Finite graph with duplicate control | No | Can be exponential / can be exponential |
| A* | Lowest $g(n)+h(n)$ | Under suitable finite-branching and positive-cost assumptions | Under heuristic and duplicate-handling conditions below | Worst case exponential; memory is a major limitation |

The deck uses $O(b^d)$ for BFS; counting generated nodes at the next layer can give $O(b^{d+1})$. Both express exponential growth. DFS's $O(bm)$ space bound is for a depth-first tree traversal; storing an explored set for graph search may require much more memory.

**Study supplement:** uniform-cost search orders by $g(n)$ and handles unequal positive costs. It is a useful baseline, although not a developed lecture section here. A* with $h=0$ behaves like uniform-cost search.

## Heuristics and A-star guarantees

$g(n)$ is the cost already paid; $h(n)$ estimates remaining cost; $f(n)=g(n)+h(n)$ estimates total solution cost through $n$.

- **Admissible:** $0\leq h(n)\leq h^*(n)$, where $h^*$ is the true cheapest remaining cost.
- **Consistent:** $h(n)\leq c(n,n')+h(n')$ for every successor, with zero at a goal.
- **Dominance:** if two heuristics are admissible and $h_2(n)\geq h_1(n)$ everywhere, $h_2$ provides at least as strong a lower bound. Exact node counts still depend on ties and implementation.

Consistency is a triangle-inequality condition and implies admissibility for states with a path to a goal. It makes $f$ nondecreasing along a path.

Admissibility supports optimal A* tree search. Graph A* can use a consistent heuristic without reopening closed states. With an admissible but inconsistent heuristic, graph A* must handle improved paths, commonly by reopening. Test for a goal when it is removed as the best frontier node, not merely when it is first generated.

Completeness also needs search-space/cost assumptions; an admissible heuristic alone does not prevent infinitely many zero-cost steps from delaying a goal.

The slide's Romania trace illustrates greedy selection toward Bucharest and A*'s route through Sibiu, Rimnicu Vilcea, and Pitesti. Straight-line distance is an intuitive lower bound for road distance when those costs share compatible units.

## Worked search example

**Study supplement: newly written graph.** Edges are directed: `S→A:2`, `S→B:1`, `A→G:2`, `B→G:9`. Let `h(S)=3`, `h(A)=2`, `h(B)=1`, `h(G)=0`.

After expanding `S`:

| Frontier state | $g$ | $h$ | $f$ |
|---|---:|---:|---:|
| A | 2 | 2 | 4 |
| B | 1 | 1 | 2 |

Greedy chooses `B`, then `G` because `h(G)=0`, returning cost 10. A* chooses `B` first but keeps `A` in the frontier. Its frontier then contains `A:f=4` and `G:f=10`. Expanding `A` improves `G` to cost 4; the final path is `S→A→G`.

BFS returns a two-edge path; with `A` generated first it returns cost 4, but a different same-depth ordering can return cost 10. Equal edge count is not equal cost. DFS's result also depends on successor order.

## A-star pseudocode

**Study supplement: supports reopening and skips stale queue entries.**

```text
best_g[start] = 0
push (h(start), 0, start) onto priority queue
while queue is not empty:
    (_, queued_g, state) = pop minimum
    if queued_g != best_g[state]: continue
    if goal(state): return reconstruct_path(state)
    for each (next, cost) in successors(state):
        candidate = queued_g + cost
        if candidate < best_g.get(next, infinity):
            best_g[next] = candidate
            parent[next] = state
            push (candidate + h(next), candidate, next)
return failure
```

Use a deterministic tie-breaker if queue entries contain state objects that cannot be compared. Better heuristics save exploration; they do not remove A*'s worst-case memory problem.
