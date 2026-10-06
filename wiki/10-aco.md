# Ant colony optimization

[Home](../README.md) · [Next: ABC](11-abc.md)

**Course sources:** `04_Optimization.pptx`, slides 12–15; Dorigo, Maniezzo, and Colorni, “Ant System: Optimization by a Colony of Cooperating Agents” (1996), PDF pages 1–13 / printed pages 29–41.

## Contents

- [Constructing solutions](#constructing-solutions)
- [Transition and pheromone formulas](#transition-and-pheromone-formulas)
- [Worked probabilities](#worked-probabilities)
- [Reading variants and conclusions](#reading-variants-and-conclusions)

## Constructing solutions

ACO is a family of methods inspired by indirect communication through pheromone trails. The original **Ant System** is a specific member of that family.

For the traveling salesperson problem, construct a closed tour visiting every city once. An artificial ant keeps a visited list, chooses feasible next cities probabilistically, evaluates the complete tour, and contributes pheromone. Better tours reinforce their edges more strongly. Evaporation reduces old information.

The visited/tabu list here prevents revisiting cities during tour construction; it is not the same mechanism as the separate tabu-search algorithm used for comparison in the paper.

## Transition and pheromone formulas

For ant k currently at city i, with allowed unvisited cities $A_k$:

$$P_k(j\mid i)=\frac{\tau_{ij}^{\alpha}\eta_{ij}^{\beta}}{\sum_{\ell\in A_k}\tau_{i\ell}^{\alpha}\eta_{i\ell}^{\beta}},\qquad j\in A_k.$$

Disallowed cities have probability zero. Here $\tau$ is learned pheromone and $\eta_{ij}=1/d_{ij}$ is a local visibility heuristic for positive distance. $\alpha$ controls trail influence and $\beta$ distance influence.

Using the **slides' evaporation-rate convention**:

$$\tau_{ij}\leftarrow(1-\rho)\tau_{ij}+\sum_k\Delta\tau_{ij}^k,$$
$$\Delta\tau_{ij}^k=\begin{cases}Q/L_k&\text{if ant k used edge }(i,j)\\0&\text{otherwise}.\end{cases}$$

$L_k$ is the entire closed-tour length and Q scales deposits. The 1996 paper instead uses its rho as a **retention factor**, writing $\rho\tau+\Delta\tau$. Thus the paper's rho equals $1-\rho_{\text{evaporation}}$; do not copy the same parameter name between formulas without translating its meaning.

```text
initialize positive trails
repeat:
    each ant constructs a feasible complete tour
    evaluate tour lengths and save best
    optionally improve tours with local search
    evaporate trails and add deposits
return best tour
```

## Worked probabilities

**Study supplement:** two allowed edges have `(pheromone, distance)` values `(2,2)` and `(1,1)`. With $\alpha=1$, $\beta=2$, their weights are $2(1/2)^2=0.5$ and $1(1)^2=1$. Therefore probabilities are $1/3$ and $2/3$. More pheromone alone does not determine the choice.

With current trail 2, evaporation rate 0.2, and total deposit 0.5, the updated trail is $0.8(2)+0.5=2.1$.

## Reading variants and conclusions

The paper contrasts three historical variants:

| Variant | Deposit timing / signal |
|---|---|
| Ant-density | Local step update with a fixed deposit |
| Ant-quantity | Local step update scaled by edge distance |
| Ant-cycle | After a complete tour, scaled by whole-tour quality |

Ant-cycle supplied better feedback in the reported comparisons because complete solution quality matters. The paper also studies distributing ants among starting cities, population size, parameter sensitivity, stagnation, and an elitist strategy reinforcing the best-so-far tour.

Its extensions include asymmetric TSP, quadratic assignment, and job-shop scheduling. The quadratic assignment objective associates facilities to locations and sums distance times flow. Job-shop construction must restrict choices to operations whose predecessors are satisfied. These applications demonstrate that feasibility logic and visibility must be adapted to the problem.

The experiments compare Ant System with simulated annealing, tabu search, and specialized TSP heuristics. They do not establish that ACO always beats those methods; the authors note the computational advantage of specialized methods in some cases. Excessive trail concentration can lead to stagnation and reduce exploration.
