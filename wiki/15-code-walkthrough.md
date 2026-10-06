# Course code walkthrough and corrections

[Home](../README.md)

**Course sources:** the three `.py` files in the ZIP. The synced workspace also contains other scripts, but they are outside this archive's source set and were not used as class-source evidence.

## Contents

- [Gradient descent example](#gradient-descent-example)
- [Animated gradient descent](#animated-gradient-descent)
- [Simulated annealing example](#simulated-annealing-example)
- [Execution and verification](#execution-and-verification)

## Gradient descent example

`gd_functions.py` defines a quadratic, its analytic gradient, eta=0.1, 1,000 iterations, and an initial zero vector. It prints every iteration and converges toward `(2,-2)`. The objective and gradient agree.

Potential improvements are a convergence tolerance and less frequent printing. A fixed iteration count is simple but may perform unnecessary updates after numerical convergence.

## Animated gradient descent

`gd_steroids.py` uses the same objective and gradient but eta=0.02 and 200 updates. It saves the trajectory, draws a 3D surface, creates a Matplotlib animation, saves `descenso_gradiente-s.mp4`, and shows the plot.

**Source inconsistency:** both the plotted surface `Z` and animated heights `zs` use `(y+1)^2`, while optimization uses `(y+2)^2`. The optimization converges toward `(2,-2)` but the drawn surface has its minimum at `(2,-1)`.

To make a working copy coherent, change the plotted surface and animation heights to:

```python
Z = (X - 2)**2 + (Y + 2)**2
zs = (xs - 2)**2 + (ys + 2)**2
```

These are suggested corrections, not edits to the original uploaded files. Video export also requires a working FFmpeg writer; NumPy and Matplotlib alone do not guarantee MP4 export.

## Simulated annealing example

`sa_functions.py` generates a random initial point within bounds, proposes a clipped random offset, applies the SA acceptance test, cools the temperature, and returns best solution, best value, and a **current-value** history. It defines both Rastrigin and Ackley, but the final invocation selects Rastrigin.

Its defaults are 100,000 iterations, initial temperature 100, and cooling multiplier 0.8. Already after 100 steps the temperature is approximately $2.04\times10^{-8}$; after roughly 3,300–3,400 steps it reaches floating-point subnormal/underflow behavior. Division by a zero or near-zero temperature can cause warnings or NaNs for equal-cost proposals. Long before that, most worse moves are effectively rejected.

**Study supplement: robust acceptance structure for a working copy.**

```python
if delta <= 0:
    accept = True
elif temperature > 0:
    accept = rng.random() < np.exp(-delta / temperature)
else:
    accept = False
```

This avoids division at zero, but does not fix an excessively fast schedule. Choose a temperature floor/stopping condition and a cooling schedule matched to the intended budget. For example, deriving gamma from a desired positive end temperature uses $\gamma=(T_{end}/T_0)^{1/N}$. This is a design illustration, not a course-specified parameter.

Clipping proposals can concentrate probability at boundaries. Record the chosen boundary policy, seed, and evaluation budget when comparing results. To plot best-so-far rather than current cost, store `best_value` each iteration.

## Execution and verification

This repository contains explanations and corrective snippets, not an altered copy of the supplied programs. The objective/gradient arithmetic and example updates were checked independently. The original animation and 100,000-step SA program were not run end-to-end; no video-export or stochastic-performance claim is made.

To run your private copies locally, use an environment with NumPy and Matplotlib; install/configure FFmpeg for the animation. For Prolog examples use the class's SWI-Prolog setup. The complete `01_Code/` directory referenced by the slides was absent from the upload.
