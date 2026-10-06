# Artificial bee colony

[Home](../README.md) · [Next: comparison guide](12-comparisons.md)

**Course source:** `04_Optimization.pptx`, slides 16–19. The lecture associates this material with Karaboga and a 2007 label; the year here is a slide label rather than an independently verified first-publication date. No dedicated ABC paper is included.

## Contents

- [Bee roles](#bee-roles)
- [Search cycle](#search-cycle)
- [Worked neighbor](#worked-neighbor)

## Bee roles

A food source represents a candidate solution and its quality represents objective/fitness information.

| Role | Computational task |
|---|---|
| Employed bees | Search around assigned sources |
| Onlookers | Select promising sources and search around them |
| Scouts | Discover new sources when old ones are abandoned |

The slides emphasize employed/onlooker exploitation and scout exploration. The main controls are number of sources, abandonment limit, and maximum cycles. The lecture's population labels should be read carefully: source count is commonly associated with employed bees, while an implementation defines how many onlookers it uses.

## Search cycle

```text
initialize sources; evaluate them
repeat:
    employed phase: propose and greedily compare neighbors
    onlooker phase: select sources by quality and search nearby
    scout phase: replace sources that exceed unsuccessful-trial limit
    remember best source
return best source
```

**Study supplement: common ABC neighbor formula, expanding the slide's index notation.**

$$v_{ij}=x_{ij}+\phi_{ij}(x_{ij}-x_{kj}),\qquad k\ne i,\quad\phi_{ij}\sim U(-1,1).$$

Choose another source k and a coordinate j, modify that coordinate, enforce bounds, and evaluate. Accept an improved source and reset its unsuccessful-trial count; otherwise increment the count. A source reaching `limit` can be replaced by a new random feasible source.

Onlookers may sample by normalized positive fitness $p_i=F_i/\sum F$. This is a common formulation rather than a formula transcribed from the uploaded slides. For minimization, define a suitable score or selection method; do not assign larger raw costs more selection probability.

## Worked neighbor

**Study supplement:** if $x_{ij}=4$, $x_{kj}=1$, and $\phi=-0.5$, then $v_{ij}=4-0.5(3)=2.5$. For objective $f(x)=x^2$, this coordinate change improves a one-dimensional candidate from 16 to 6.25 and is accepted.

A small limit increases replacement and exploration but may abandon useful sources early. A large limit spends more effort refining existing sources but can prolong stagnation. ABC, like the other finite-run metaheuristics here, does not promise a global optimum for every problem.
