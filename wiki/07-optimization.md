# Optimization, gradient descent, and simulated annealing

[Home](../README.md) · [Next: genetic algorithms](08-genetic-algorithms.md)

**Course sources:** `04_Optimization.pptx`, slides 2–4; `gd_functions.py`, `gd_steroids.py`, `sa_functions.py`. Pseudocode and convergence analysis are study supplements.

## Contents

- [Optimization problems](#optimization-problems)
- [Gradient descent](#gradient-descent)
- [Simulated annealing](#simulated-annealing)
- [Benchmark functions](#benchmark-functions)
- [Evaluation practice](#evaluation-practice)

## Optimization problems

Optimization chooses a feasible candidate minimizing or maximizing an objective:

$$x^*=\arg\min_{x\in\mathcal F}f(x).$$

A **local minimum** is best within a neighborhood; a **global minimum** is best across the whole feasible space. Multiple global minimizers can exist. Maximization can be converted to minimization of $-f$.

Continuous optimization chooses numerical coordinates. Combinatorial optimization chooses structures such as routes, assignments, or schedules. Representation and constraints determine which operators make sense.

**Exploration** investigates new regions. **Exploitation** improves promising regions. Too much exploitation risks premature convergence; too much exploration wastes evaluations and may prevent refinement.

## Gradient descent

For a differentiable objective, update opposite the gradient:

$$\mathbf w_{t+1}=\mathbf w_t-\eta\nabla f(\mathbf w_t).$$

$\eta$ is the learning rate. The course program uses

$$f(x,y)=(x-2)^2+(y+2)^2,\qquad\nabla f=(2(x-2),2(y+2)).$$

Its unique minimum is $(2,-2)$ with value zero. Starting at $(0,0)$ with $\eta=0.1$ gives gradient $(-4,4)$ and next point $(0.4,-0.4)$, with $f=5.12$ rather than the initial 8.

For this particular quadratic the error obeys $e_{t+1}=(1-2\eta)e_t$. Thus convergence occurs for $0<\eta<1$. At $\eta=0.5$ the minimizer is reached in one step; at $\eta=1$ the error oscillates without shrinking. This learning-rate interval is not universal for other objectives.

```text
initialize w
repeat until stopping condition:
    gradient = grad_f(w)
    w = w - learning_rate * gradient
return w
```

GD is efficient for smooth problems with useful gradients. It does not generally guarantee a global solution on a nonconvex landscape. Convexity, step size, smoothness, and stopping conditions determine stronger guarantees.

## Simulated annealing

SA keeps one current solution, proposes a random neighbor, and sometimes accepts a worse one to escape local minima. For minimization let $\Delta=f(x')-f(x)$:

$$P(\text{accept})=\begin{cases}1&\Delta\leq0\\e^{-\Delta/T}&\Delta>0.\end{cases}$$

The course implementation uses strict improvement in the first branch; equal-cost moves still have probability one when the temperature is positive. Temperature controls willingness to accept deterioration. With $\Delta=2$, at $T=10$ the probability is about 0.819; at $T=0.5$ it is about 0.0183.

```text
initialize current, best, positive T
repeat:
    propose bounded neighbor
    delta = f(neighbor) - f(current)
    accept improvements; otherwise accept with exp(-delta/T)
    if current improves best: save it
    cool temperature
return best
```

Geometric cooling uses $T_{t+1}=\gamma T_t$, $0<\gamma<1$. Fast cooling reduces exploration quickly. General theoretical convergence results require additional assumptions and slow schedules; a finite run with geometric cooling has no universal global-optimum guarantee.

The course script proposes a vector offset uniformly in `[-1,1]`, clips it to bounds, tracks current values in history, and retains a separate best. Its 100,000 iterations with $T_0=100$ and $\gamma=0.8$ cause temperature to become numerically negligible and eventually underflow. This is a practical defect discussed in the [code walkthrough](15-code-walkthrough.md).

## Benchmark functions

The SA script optimizes Rastrigin:

$$f(\mathbf x)=10D+\sum_{i=1}^{D}\left[x_i^2-10\cos(2\pi x_i)\right].$$

Its global minimum is zero at the zero vector, but its many local minima make exploration important. The script uses two-dimensional bounds $[-5.12,5.12]^2$.

It also defines, but does not select for the final call, the 2D Ackley function:

$$f(x,y)=-20e^{-0.2\sqrt{(x^2+y^2)/2}}-e^{(\cos(2\pi x)+\cos(2\pi y))/2}+e+20.$$

Its minimum is zero at $(0,0)$, subject to floating-point roundoff. Defining a function does not mean the program actually optimizes it.

## Evaluation practice

Compare algorithms using the same objective, bounds, and evaluation budget. For stochastic methods run multiple seeds and report best/mean/spread, success criteria, and time or objective evaluations. A best-so-far curve is monotone for minimization; a current-solution curve can rise under SA. A single attractive run is not evidence of a universal ranking.
