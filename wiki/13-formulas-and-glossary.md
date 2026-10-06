# Formula sheet and glossary

[Home](../README.md)

**Source basis:** formulas explained in linked chapters. GD/SA come from supplied code; A* and minimax from the search deck; ACO from the optimization images and reading. Perceptron/SVM, explicit inertia PSO, ABC neighbor, and GA selection notation are study supplements.

## Contents

- [Formula sheet](#formula-sheet)
- [Glossary](#glossary)

## Formula sheet

| Concept | Formula / condition | Interpretation |
|---|---|---|
| A* | $f(n)=g(n)+h(n)$ | Total estimated path cost |
| Admissibility | $0\leq h(n)\leq h^*(n)$ | Never overestimate cheapest remaining cost |
| Consistency | $h(n)\leq c(n,n')+h(n')$ | Heuristic triangle inequality |
| Minimax | MAX uses max, MIN uses min | Back up values from leaves |
| Alpha–beta | Prune if $\alpha\geq\beta$ | No influence on ancestor decision |
| N-queens | $Q_i\ne Q_j$, $|Q_i-Q_j|\ne|i-j|$ | Columns and diagonals safe |
| Horn rule | $A\land B\Rightarrow C$ | `c :- a, b.` |
| GD | $w'=w-\eta\nabla f(w)$ | Descend opposite gradient |
| Quadratic gradient | $(2(x-2),2(y+2))$ | Supplied GD example |
| Worse SA move | $P=e^{-\Delta/T}$ | Acceptance for $\Delta>0$, $T>0$ |
| Cooling | $T_t=T_0\gamma^t$ | Geometric schedule |
| Proportional selection | $p_i=F_i/\sum_jF_j$ | Requires suitable nonnegative scores and positive denominator |
| Binary mutation | Expected flips $=Lp_m$ | Independent per-bit mutation |
| PSO velocity | $v'=\omega v+c_1r_1(p-x)+c_2r_2(g-x)$ | Inertia-weight variant |
| PSO position | $x'=x+v'$ | Move after updating velocity |
| ACO visibility | $\eta_{ij}=1/d_{ij}$ | Favor short positive-distance edges |
| ACO choice | Weight $=\tau_{ij}^{\alpha}\eta_{ij}^{\beta}$ | Normalize over feasible cities |
| ACO update | $\tau'=(1-\rho)\tau+\sum_k\Delta\tau^k$ | Slides' evaporation convention |
| Ant-cycle deposit | $Q/L_k$ on used edges | Reward short complete tours |
| ABC neighbor | $v_{ij}=x_{ij}+\phi(x_{ij}-x_{kj})$ | Perturb using another source |
| Perceptron | $\hat y=\mathbb1[w^Tx+b\geq0]$ | Linear threshold |
| Hard-margin SVM | Minimize $\frac12\|w\|^2$ with $y_i(w^Tx_i+b)\geq1$ | Maximum margin for separable data |

**Notation warning:** eta is GD learning rate in one chapter but ACO visibility in another. Alpha/beta are pruning bounds in games but influence exponents in ACO. Rho is an evaporation rate in slides and a retention factor in the 1996 paper. Read the local definitions.

## Glossary

| Term | Meaning |
|---|---|
| Actuator | Mechanism through which an agent acts |
| Admissible heuristic | Lower-bound estimate of remaining solution cost |
| Agent | Entity perceiving and acting on an environment |
| Arity | Number of arguments of a predicate or functor |
| Backtracking | Undo a choice and try another |
| Chromosome | Encoded candidate solution |
| Closed-world assumption | Treat non-derivable information as false in the relevant KB |
| Complete algorithm | Finds a solution when one exists under stated assumptions |
| Consistent assignment | Violates no constraint |
| CSP | Variables, domains, and constraints defining valid assignments |
| Fitness | Score determining candidate preference |
| Frontier | Generated search nodes not yet expanded |
| Global optimum | Best value over the feasible space |
| Gradient | Vector of partial derivatives |
| Heuristic | Problem-informed estimate guiding search |
| Horn clause | Clause with at most one positive literal |
| Local optimum | Best value relative to a neighborhood |
| Metaheuristic | General search framework adaptable to optimization problems |
| Optimal algorithm | Returns a best-quality solution under its conditions |
| PEAS | Performance, Environment, Actuators, Sensors |
| Pheromone | Shared learned attraction signal in ACO |
| Rationality | Selecting actions expected to best satisfy performance goals given evidence |
| State graph | Problem states and transitions |
| Search tree | Explored paths, possibly repeating the same state |
| Unification | Binding variables to make terms identical |
| Utility | Numerical preference over outcomes |
