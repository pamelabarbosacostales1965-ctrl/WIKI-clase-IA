# Particle swarm optimization

[Home](../README.md) · [Next: ACO](10-aco.md)

**Course sources:** `04_Optimization.pptx`, slides 8–11; Kennedy and Eberhart, “Particle Swarm Optimization” (1995), uploaded PDF pages 1–7.

## Contents

- [Particle state](#particle-state)
- [Update rule](#update-rule)
- [Worked update](#worked-update)
- [The original reading](#the-original-reading)

## Particle state

PSO searches using particles moving through a numerical solution space. Particle i has a position $x_i$, velocity $v_i$, and its best historical position $p_i$. The global-best version shares the best historical swarm position $g$.

Personal memory encourages return to successful individual positions. Social information encourages movement toward successful swarm positions. Random factors keep the response from being identical for every particle.

## Update rule

**Study supplement: standard inertia-weight notation.** The original 1995 paper predates this explicit inertia-weight variant; the slide identifies cognitive and social components.

$$v_i^{t+1}=\omega v_i^t+c_1r_1(p_i-x_i^t)+c_2r_2(g-x_i^t),$$
$$x_i^{t+1}=x_i^t+v_i^{t+1}.$$

$\omega$ retains momentum, $c_1$ weights the cognitive term, $c_2$ the social term, and independent random values $r_1,r_2\sim U(0,1)$ are normally sampled by particle, dimension, and update. The lecture's $\alpha_1\phi_1$ and $\alpha_2\phi_2$ express the same types of attraction.

```text
initialize positions and velocities
evaluate; initialize personal and global bests
repeat:
    for each particle:
        update velocity and position
        enforce boundary policy
        evaluate
        update personal best if improved
    update global best
return global best
```

The boundary policy may clamp positions, reflect motion, or use another defined method. It changes behavior. The returned global best is a stored successful position, not necessarily the final position of a particular particle.

## Worked update

**Study supplement:** in one dimension let $x=3$, $v=0.2$, $p=2$, $g=1$, $\omega=0.5$, $c_1=c_2=1$, $r_1=0.4$, $r_2=0.6$.

$$v'=0.1+0.4(2-3)+0.6(1-3)=-1.5,\qquad x'=1.5.$$

The step moves toward the remembered good positions. Only objective evaluation can determine whether it is better. Momentum can cause overshoot, which may aid exploration or cause instability.

## The original reading

The paper follows the development from flocking simulation to optimization: nearest-neighbor velocity matching, random “craziness,” attraction to a remembered food location, and eventual removal of unnecessary simulation components. Personal and shared bests retain the useful optimization behavior.

Its early update retains velocity and adds randomized attraction terms; it also experiments with changes to those terms and velocity limits. Therefore one should not silently attribute all later PSO variants to that single original formulation.

The reading discusses nonlinear continuous benchmarks and neural-network weight training, including Schaffer's f6 and an XOR example. Its successful reported trials are evidence for the tested setups, not a universal global-convergence result.

Compared with a GA, basic PSO does not breed and replace chromosomes using crossover and mutation. It updates existing particle trajectories and shares memory. It can converge prematurely, especially when strong social attraction collapses diversity. Topology, coefficients, initialization, and bounds matter.
