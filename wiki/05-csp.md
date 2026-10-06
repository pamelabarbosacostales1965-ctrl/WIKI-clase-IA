# Constraint satisfaction problems

[Home](../README.md) · [Next: logic and Prolog](06-logic-and-prolog.md)

**Course sources:** `02_Problem Solving.pptx`, slides 23–25; Prolog deck, slides 25–27.

## Contents

- [Modeling a CSP](#modeling-a-csp)
- [Backtracking and pruning](#backtracking-and-pruning)
- [N-queens](#n-queens)

## Modeling a CSP

A CSP is described by variables $X=\{X_1,\ldots,X_n\}$, domains $D_i$, and constraints $C$. A solution assigns every variable a value and satisfies every constraint. A consistent partial assignment violates no applicable constraint; it need not be complete.

Sudoku assigns digits to cells and forbids repeated digits in rows, columns, and boxes. Scheduling assigns times or resources while enforcing conditions such as no overlap or an activity occurring before another.

**Study supplement: map coloring.** Let regions A, B, C form a triangle, each with domain `{red, blue, green}`. Constraints are `A != B`, `B != C`, `A != C`. Assignment `(red, blue, green)` is complete and consistent. `(red, red, green)` is complete but inconsistent.

## Backtracking and pruning

Backtracking builds an assignment one variable at a time and reverses a choice when it cannot lead to a solution. The image on slide 25 includes variable selection, value ordering, inference, and undoing both assignments and inferred domain changes.

**Study supplement: expansion of terms listed in the lecture.**

| Technique | What it does | Example |
|---|---|---|
| Minimum remaining values (MRV) | Select the unassigned variable with the smallest current domain | Choose a cell with two candidates before one with five |
| Forward checking | Remove values inconsistent with a new assignment from neighboring unassigned variables | After A=red, remove red from B and C |
| Arc consistency | Require every remaining value to have supporting values across each binary constraint | Delete B=blue if C's only value is blue and B != C |
| Least constraining value | Try a value that removes fewest neighbor choices | Supplementary value-ordering heuristic |

Arc consistency is stronger than checking only the newly assigned variable, but does not guarantee a global solution. A triangle with two colors can be arc-consistent before assignment yet unsatisfiable.

```text
BACKTRACK(assignment, domains):
    if complete: return assignment
    choose variable (for example, MRV)
    for value in its current domain:
        if consistent with assignment:
            save domain changes
            assign value and propagate constraints
            if no domain is empty:
                result = BACKTRACK(updated assignment, updated domains)
                if result succeeds: return result
            undo assignment and domain changes
    return failure
```

## N-queens

Let $Q_i$ be the column of the queen in row $i$, with domain $\{1,\ldots,N\}$. There is one queen per row by representation. For distinct rows $i,j$:

$$Q_i\ne Q_j,\qquad |Q_i-Q_j|\ne|i-j|.$$

Distinct columns prevent column attacks; the absolute-difference condition prevents diagonal attacks. For $N=4$, `[2,4,1,3]` is a solution.

The Prolog lecture contrasts generating an entire permutation and then testing it with testing diagonal safety as each queen is placed. Early checks cut off entire invalid subtrees. The deck reports increasingly large inference-count reductions as N grows; these depend on the implementation and should not be treated as universal speed ratios.

The listed solution counts are 2 for N=4, 10 for N=5, 4 for N=6, 40 for N=7, and 92 for N=8. These count all solutions including symmetric variants. N=2 and N=3 have no solution.
