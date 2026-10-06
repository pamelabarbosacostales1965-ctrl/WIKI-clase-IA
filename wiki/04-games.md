# Adversarial search and games

[Home](../README.md) · [Next: CSPs](05-csp.md)

**Course source:** `02_Problem Solving.pptx`, slides 17–22.

## Contents

- [Minimax](#minimax)
- [Alpha–beta pruning](#alphabeta-pruning)
- [Worked class tree](#worked-class-tree)

## Minimax

In a two-player zero-sum game, MAX prefers larger utility and MIN prefers smaller utility. The class model assumes deterministic transitions and perfect information. A solution is a strategy that accounts for the opponent, not simply a fixed path.

$$V(s)=\begin{cases}
U(s)&\text{if terminal}\\
\max_{s'\in Succ(s)}V(s')&\text{if MAX plays}\\
\min_{s'\in Succ(s)}V(s')&\text{if MIN plays}.
\end{cases}$$

The utility must always use the same player's perspective. Minimax assumes optimal opposition. For branching factor $b$ and search depth $m$, full minimax takes $O(b^m)$ time; a depth-first traversal uses $O(bm)$ working space.

**Study supplement:** when a full game tree is impractical, stop at a depth limit and use an evaluation function. The result is optimal for the evaluated finite tree, not necessarily the actual whole game. Chess-like evaluations are estimates, while terminal utilities describe actual outcomes.

## Alpha–beta pruning

Alpha–beta calculates the same minimax value while skipping branches that cannot affect the backed-up result.

- $\alpha$: a lower bound MAX can already secure.
- $\beta$: an upper bound MIN can already enforce.
- Prune when $\alpha\geq\beta$.

At MAX update $\alpha=\max(\alpha,v)$; at MIN update $\beta=\min(\beta,v)$. Start with $\alpha=-\infty$, $\beta=+\infty$.

Worst-case time remains $O(b^m)$. With excellent move ordering, the ideal bound is about $O(b^{m/2})$. Good ordering changes efficiency, not the minimax value; equally valued moves may be chosen differently under different tie rules.

## Worked class tree

The slide 19 root is MAX, with three MIN children:

| MIN branch | Leaf utilities | Backed-up value |
|---|---|---:|
| B | 3, 12, 8 | 3 |
| C | 2, 4, 6 | 2 |
| D | 14, 5, 2 | 2 |

The root chooses B and has value $\max(3,2,2)=3$.

With left-to-right alpha–beta, B first establishes $\alpha=3$. At C, the first leaf gives $\beta=2$; since $2\leq3$, skip leaves 4 and 6. D must inspect 14, then 5, then 2 under this ordering. Its final value is 2 and cannot improve MAX's decision.

**Exam trap:** pruning does not claim the skipped leaves are bad in isolation. It claims they cannot change the ancestor's decision given already available alternatives.
