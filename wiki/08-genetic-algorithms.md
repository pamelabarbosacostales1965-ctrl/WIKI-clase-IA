# Genetic algorithms

[Home](../README.md) · [Next: PSO](09-pso.md)

**Course sources:** `04_Optimization.pptx`, slides 2–7; John H. Holland, “Genetic Algorithms” (1992), uploaded PDF pages 2–8 / printed pages 66–72. The last PDF page contains advertising rather than additional core algorithm content.

## Contents

- [Representation and operators](#representation-and-operators)
- [One generation](#one-generation)
- [Hollands reading](#hollands-reading)
- [Strengths and limitations](#strengths-and-limitations)

## Representation and operators

A GA maintains a population of candidate solutions. Selection favors useful candidates; crossover combines parent information; mutation introduces variation. The lecture emphasizes variation, selection, and heredity.

| Term | Computational meaning |
|---|---|
| Individual / chromosome | Encoded candidate |
| Gene | Part of the representation |
| Fitness | Score used to favor candidates |
| Selection | Choose parents or survivors |
| Crossover | Exchange or combine parental segments |
| Mutation | Random modification |
| Generation | Population update cycle |

The deck uses binary chromosomes encoding numerical values. **Study supplement:** GAs can also use real vectors, permutations, or trees; their operators must preserve or repair validity. Ordinary bit crossover is unsuitable for a route permutation if it duplicates cities.

## One generation

```text
initialize population
evaluate candidates
repeat:
    select parents
    create offspring with crossover
    mutate offspring
    evaluate offspring
    form next population (optionally preserve elite)
return best candidate found
```

**Study supplement: binary example.** Maximize the number of 1s in a four-bit chromosome. `1010` and `0111` have fitness 2 and 3. Crossover after two bits gives `10|11` and `01|10`, or `1011` and `0110`. Flipping the second bit of `1011` produces `1111`, whose fitness is 4. This illustrates the operators; it does not claim mutation will reliably improve fitness.

For positive fitness scores, proportional selection can use

$$P(i)=\frac{F_i}{\sum_j F_j}.$$

Raw minimization costs must not be used directly in that formula because larger costs would be favored. Tournament or rank selection avoids requiring a specific positive-score transformation. With independent per-bit mutation probability $p_m$ and length $L$, the expected number of flipped bits is $Lp_m$.

**Elitism** copies selected best candidates forward and preserves their quality, but excessive elitism can reduce diversity. It is a study supplement to the lecture's basic cycle.

## Hollands reading

Holland describes evolving encoded rules and designs when hand-specifying the full solution is difficult. His reading adds several ideas beyond the slides:

- **Schemas / building blocks:** a pattern such as `1*0*` describes a family of chromosomes; `*` means either bit. Favorable short patterns can be recombined.
- **Implicit parallelism:** one chromosome belongs to many pattern-defined regions, so population processing also samples many schemas. This is a theoretical perspective, not literal exhaustive evaluation of every solution.
- **Gene interactions:** a combination's fitness may differ greatly from the sum of its parts. A locally promising building block need not combine well with all others.
- **Inversion:** rearranging gene order can place related elements closer and change crossover disruption.
- **Classifier systems:** condition/action rules compete and receive credit; useful rules can reproduce and adapt to unfamiliar situations.
- **Examples:** evolving repeated prisoner's-dilemma strategies and designing turbine components illustrate optimization of structured behavior and engineering parameters.

**Study supplement:** schema order counts fixed positions; defining length is the span between the first and last fixed position. Under single-point crossover, a long-spanning pattern has more opportunities for disruption than a compact one. Favorable schema propagation is not a proof that a GA always reaches the global optimum.

## Strengths and limitations

GAs work without derivatives and can suit difficult structured spaces when a sensible encoding and fitness exist. Costs include many evaluations, representation design, parameter tuning, loss of diversity, and handling constraints. Biological inspiration explains the mechanism; empirical performance must still be measured.
