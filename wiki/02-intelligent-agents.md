# Intelligent agents

[Home](../README.md) · [Next: search](03-search.md)

**Course source:** `03_Intelligent Agents.pptx`, slides 2–18, including image tables on slides 7 and 13.

## Contents

- [Agent function and rationality](#agent-function-and-rationality)
- [PEAS](#peas)
- [Environment dimensions](#environment-dimensions)
- [Agent architectures](#agent-architectures)
- [State representations](#state-representations)

## Agent function and rationality

An **agent** perceives its environment through sensors and acts through actuators. The lecture's slide 2 begins with proposition definitions, but its human, robot, and software examples illustrate the agent concept.

The **agent function** maps a percept history to an action. An **agent program** implements an approximation of that function on an architecture. A table for all histories becomes enormous, so useful programs exploit structure, memory, or learning.

In the vacuum world, the agent observes its location and whether that room is dirty. Actions are left, right, and vacuum. A simple rule is “if dirty, vacuum; otherwise move to the other room.” This does not require a table containing every possible percept history.

A **rational agent** chooses the action expected to perform best given its percepts, knowledge, and available actions. Rationality is about the decision using available evidence, not guaranteed success or knowledge of future outcomes. Information gathering can be rational when it improves later decisions.

**Study supplement:** for outcomes $s'$ and utility $U$,

$$a^*=\arg\max_a\sum_{s'}P(s'\mid a,\text{information})U(s').$$

The designer supplies a performance measure. Rewarding only the number of vacuum actions can encourage repeated unnecessary cleaning. Rewarding cleanliness while charging for energy better reflects the desired behavior.

## PEAS

PEAS means **Performance, Environment, Actuators, Sensors**. Define it before choosing an architecture.

**Study supplement: worked taxi example.**

| Component | Specification |
|---|---|
| Performance | Safe arrival, legal driving, reasonable journey time, passenger comfort |
| Environment | Roads, traffic, weather, passengers, pedestrians |
| Actuators | Steering, accelerator, brakes, signals |
| Sensors | Cameras, positioning, speed and proximity sensing |

Do not confuse a performance criterion such as safe travel with an actuator such as braking.

## Environment dimensions

| Dimension | First case | Second case | Design consequence |
|---|---|---|---|
| Observability | Fully observable: relevant state available | Partially observable: information missing | Maintain beliefs or internal state |
| Dynamics of outcomes | Deterministic | Stochastic / nondeterministic | Reason about uncertain outcomes |
| Dependence between decisions | Episodic | Sequential | Plan for later consequences |
| Change during deliberation | Static | Dynamic | Account for time and react promptly |
| State/action values | Discrete | Continuous | Choose suitable representation and algorithms |
| Other decision makers | Single agent | Multi-agent | Consider cooperation or competition |

**Semidynamic:** the world is unchanged while thinking, but the performance measure changes; chess with a clock is the class example. Nondeterminism is broader than randomness: another agent's unknown decision may also make outcomes uncertain.

**Study supplement:** ordinary chess without a clock is fully observable, deterministic, sequential, static, discrete, and competitive multi-agent. Driving is typically partially observable, uncertain, sequential, dynamic, continuous in important variables, and multi-agent. Classifications depend on the chosen model.

## Agent architectures

| Type | Uses | Advantage | Limitation |
|---|---|---|---|
| Simple reflex | Current percept and condition–action rules | Fast and simple | No memory for hidden state |
| Model-based reflex | Internal state and a model of changes | Handles incomplete observations | Depends on model and state estimation |
| Goal-based | Desired states plus planning/search | Can adapt to changed goals | Goals alone do not rank successful outcomes |
| Utility-based | Preferences and outcome probabilities | Compares tradeoffs and uncertainty | Requires a suitable utility model |

A simple reflex program can succeed in some partially observable tasks if its current percept contains everything needed for that decision; the lecture's broad warning should be read with that qualification. A learning capability can improve any of these designs rather than replacing their decision structure.

## State representations

- **Atomic:** an indivisible state label, such as a search node `S`.
- **Factored:** a collection of attributes, such as `location=A`, `dirty_A=true`, `dirty_B=false`.
- **Structured:** objects and relationships, such as `parent(ana, sofia)`.

Richer representations allow more expressive reasoning but can increase computational effort. A CSP makes attributes explicit; Prolog makes relationships explicit.
