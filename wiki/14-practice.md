# Practice questions and answers

[Home](../README.md)

**Study supplement:** original questions based on the supplied topics, not a prediction of the exam.

## Contents

- [Questions](#questions)
- [Answers](#answers)

## Questions

1. A delivery robot cannot see behind a wall. Which environmental dimension matters, and what agent capability helps?
2. Give the five parts of a route-search formulation.
3. A path with two edges costs 20 and a path with three edges costs 6. Does BFS guarantee cost 6?
4. Why can DFS fail to terminate even when a goal exists?
5. If A has `(g,h)=(7,1)` and B has `(2,4)`, which does greedy choose and which does A* choose?
6. Is h=12 admissible when the cheapest remaining cost is 10?
7. Why can graph A* need to reopen a state?
8. A MAX root has MIN children with leaves `[5,9]` and `[3,20]`. What is its minimax value? What can be pruned left-to-right?
9. Distinguish a complete assignment from a consistent one.
10. Does arc consistency guarantee a solution for a two-color triangle?
11. Translate “if X is a parent of Y and Y is a parent of Z, X is a grandparent of Z” into Prolog.
12. What substitution unifies `pair(a,Y)` and `pair(X,b)`?
13. Compare `X=2+3`, `X is 2+3`, and `2+3 =:= 5`.
14. Why is `\+ parent(X,ana)` not a query listing everyone who is not Ana's parent?
15. Why does mutual membership not prove two lists are permutations?
16. Why can logically equivalent recursive programs behave differently?
17. For $f=(x-2)^2+(y+2)^2$, calculate the first GD step from zero with eta=0.1.
18. SA proposes a cost increase of 3 at temperature 2. What is acceptance probability?
19. Why must a minimization cost not be used directly as proportional GA fitness?
20. Cross `1100` and `0011` after two bits. Give the offspring.
21. In PSO, identify personal versus social memory and explain why global best need not equal a final particle position.
22. With $x=3,v=0.2,p=2,g=1,\omega=0.5,c_1=c_2=1,r_1=0.4,r_2=0.6$, compute the PSO step.
23. ACO choices have weights 2 and 6. What are their probabilities? What if a city is already visited?
24. With evaporation rate 0.25, current trail 4, and total deposit 1, calculate the new trail.
25. What is the rho convention difference between slides and the Dorigo paper?
26. What does an ABC scout do, and what does `limit` control?
27. Can one successful stochastic run prove an algorithm is universally best?
28. Which original code visualization mismatch could mislead a GD reader?
29. What is the lecture's Fibonacci seed convention?
30. Explain one example of rational information gathering.

## Answers

1. Partial observability; internal state or beliefs and possibly active sensing help.
2. Initial state, actions, transition model, goal test, cost.
3. No. BFS minimizes edge count under equal costs, not arbitrary weighted cost.
4. It may follow an infinite branch or cycle without reaching an alternative branch.
5. Greedy picks A (h=1); A* picks B (f=6 versus 8).
6. No: 12 overestimates 10.
7. An inconsistent heuristic may allow a better route to an already expanded state.
8. First MIN=5, second MIN=3, root=5. After seeing 3 in the second branch, prune 20.
9. Complete assigns all variables; consistent satisfies applicable constraints. Neither implies the other.
10. No. Each value has pairwise support, but the three inequalities cannot all hold with two colors.
11. `grandparent(X,Z) :- parent(X,Y), parent(Y,Z).`
12. X=a and Y=b.
13. First binds an expression term; second binds 5; third succeeds by numeric comparison.
14. Negation checks whether any proof exists; it does not construct a complement domain.
15. It ignores multiplicity: `[1,1,2]` and `[1,2,2]` pass mutual membership.
16. Clause and goal order control depth-first proof search and may introduce nontermination.
17. Gradient=(-4,4), next=(0.4,-0.4), cost=5.12.
18. $e^{-3/2}\approx0.2231$.
19. Higher raw cost would receive more selection probability, favoring worse candidates.
20. `1111` and `0000`.
21. Personal best stores one particle's best experience; global best stores the swarm's best historical experience. Particles can move away afterward.
22. Velocity=-1.5, position=1.5.
23. 0.25 and 0.75. A disallowed visited city gets zero probability and is excluded from normalization.
24. $0.75(4)+1=4$.
25. Slides: rho is evaporated fraction. Paper: rho is retained fraction.
26. It replaces an abandoned source with a new one; limit controls unsuccessful trials before abandonment.
27. No. Repeat comparable runs with shared budgets and report variability.
28. `gd_steroids.py` optimizes `(y+2)^2` but draws `(y+1)^2`.
29. F(0)=F(1)=1, so F(10)=89.
30. A robot may first scan an obscured corridor because the information improves its later route decision, even if scanning has a small immediate cost.
