# AI foundations and history

[Home](../README.md) · [Next: agents](02-intelligent-agents.md)

**Course source:** `01_Introduction to Artificial Intelligence.pptx`, slides 1–19. Historical labels below summarize the lecture; disputed details are identified in [References](../REFERENCES.md).

## Contents

- [Intelligence and models](#intelligence-and-models)
- [Historical ideas](#historical-ideas)
- [Learning models](#learning-models)
- [Correlation and causation](#correlation-and-causation)
- [Check your understanding](#check-your-understanding)

## Intelligence and models

The lecture associates intelligence with understanding, solving problems, knowledge, skill, and experience. AI asks how to make computational systems exhibit such capabilities. A system may reason with explicit rules, learn parameters from examples, or search through possible actions.

A **model** is a mathematical description or hypothesis about a system. Models make assumptions and omit details. Their usefulness depends on whether their predictions or decisions suit the task.

| Approach | What represents knowledge? | Lecture examples |
|---|---|---|
| Formal / symbolic | Statements, rules, relations | First-order logic, lambda calculus, temporal logic, rewriting |
| Statistical | Parameters and dependencies estimated from data | Regression, classification, Bayesian and Markov networks |
| Causal | Assumptions about cause-and-effect structure | Directed acyclic graphs and causal calculus |

**Study supplement:** an expert-system rule might say that a symptom combination supports a diagnosis. A statistical classifier learns associations from labeled cases. A causal model asks how an intervention would change an outcome. These answer different questions.

## Historical ideas

| Lecture milestone | Why it matters |
|---|---|
| Talos and ancient automata imagery | Humans imagined autonomous artifacts long before digital computers |
| Antikythera mechanism | Mechanical computation can predict astronomical phenomena |
| Jaquet-Droz automata and the Mechanical Turk | Apparent intelligent behavior requires examining the mechanism; the Turk concealed a human operator |
| Zuse's Z1 and ENIAC | Mechanical/electronic computation preceded modern AI systems |
| Turing test, 1950 | An operational test based on conversational behavior |
| FORTRAN and LISP | Numerical imperative programming versus symbolic list processing and recursion |
| Dartmouth, 1956 | AI became an explicit research agenda involving language, abstraction, learning, and self-improvement |
| Perceptron, 1958 | A trainable computational neuron |
| Prolog | Logic becomes an executable representation of relations |
| Backpropagation | Efficiently computes gradients for multilayer networks |
| SVM and deep learning | Margin-based classification and learning through multiple layers |
| Causal models and generative AI / LLMs | Later directions mentioned in the timeline |

The lecture's historical timeline is an overview, not a reliable source for every first-invention date. In particular, its Prolog slide mixes an imperative-language description with logic programming. Use the Prolog deck's Colmerauer/Roussel account for that language.

### Turing test

An interrogator communicates through text with a human and a machine and attempts to tell them apart. The test focuses on observable linguistic behavior. **Study supplement:** passing a conversational test does not establish infallibility, consciousness, or correctness on every task.

## Learning models

**Study supplement: formulas expanding the lecture's model overview.**

A perceptron forms a weighted sum and applies a threshold:

$$z=\mathbf{w}^{T}\mathbf{x}+b,\qquad \hat y=\mathbb{1}[z\geq0].$$

The weights encode what the unit has learned. A single linear threshold cannot separate XOR: the positive points `(0,1)` and `(1,0)` lie on opposite corners from the negative points `(0,0)` and `(1,1)`.

A multilayer network combines weighted transformations and nonlinear activations. **Backpropagation computes derivatives** using the chain rule; an optimizer such as gradient descent uses those derivatives to update weights. These are distinct operations.

An SVM seeks a separating hyperplane with a large margin. For a linearly separable hard-margin problem:

$$\min_{\mathbf w,b}\frac12\|\mathbf w\|^2\quad\text{subject to }y_i(\mathbf w^T\mathbf x_i+b)\geq1.$$

The margin width is $2/\|\mathbf w\|$. This formulation supplements the slide's margin discussion; soft margins and kernels are outside the developed class content in this upload.

Deep learning uses multiple layers to learn representations. Depth alone does not guarantee useful learning: the data, loss, architecture, and optimization still matter.

## Correlation and causation

The lecture's image examples warn that visual resemblance and statistical association can mislead. A model might confuse muffins with dogs because image features overlap.

Correlation means variables vary together. Causation concerns what produces a change. A common cause can generate an association without either observed variable causing the other. A causal DAG encodes directed causal assumptions and contains no directed cycle.

**Study supplement:** ice-cream sales and sunburn can both increase in hot weather. Changing ice-cream sales need not change sunburn. An observational conditional probability and an intervention probability answer different questions. Real systems can have feedback over time; a DAG represents an acyclic model, not a claim that every real relationship lacks feedback.

## Check your understanding

Explain why a fluent answer can still be false, why XOR challenges a single perceptron, and why fitting a statistical association does not by itself identify a causal effect.
