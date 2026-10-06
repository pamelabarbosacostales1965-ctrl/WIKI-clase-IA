# CMP 4004E Artificial Intelligence Study Wiki

An English study wiki for Daniel Riofrío Almeida's Artificial Intelligence class, prepared from the uploaded course archive. Start here, then follow the numbered chapters. This is a Markdown repository: it works in GitHub's normal file browser without enabling the separate GitHub Wiki feature.

[Read the published GitHub Wiki](https://github.com/pamelabarbosacostales1965-ctrl/WIKI-clase-IA/wiki)

## Table of contents

1. [Course overview and study route](wiki/00-course-overview.md)
2. [AI foundations and history](wiki/01-ai-foundations.md)
3. [Intelligent agents](wiki/02-intelligent-agents.md)
4. [Problem formulation and search](wiki/03-search.md)
5. [Adversarial search and games](wiki/04-games.md)
6. [Constraint satisfaction problems](wiki/05-csp.md)
7. [Logic, inference, and Prolog](wiki/06-logic-and-prolog.md)
8. [Optimization, gradient descent, and simulated annealing](wiki/07-optimization.md)
9. [Genetic algorithms](wiki/08-genetic-algorithms.md)
10. [Particle swarm optimization](wiki/09-pso.md)
11. [Ant colony optimization](wiki/10-aco.md)
12. [Artificial bee colony](wiki/11-abc.md)
13. [Algorithm comparison guide](wiki/12-comparisons.md)
14. [Formula sheet and glossary](wiki/13-formulas-and-glossary.md)
15. [Practice questions and answers](wiki/14-practice.md)
16. [Course code walkthrough and corrections](wiki/15-code-walkthrough.md)

## Sources and scope

- [Complete file inventory and topic map](SOURCE_INVENTORY.md): all 13 files, counts, checksums, and coverage.
- [References and source corrections](REFERENCES.md): exact source names and slide/page locators.
- [GitHub upload and invitation instructions](GITHUB_SHARING.md): including `@danielriofrio`.
- [Maintenance guide](CONTRIBUTING.md): how to add future class material.

The archive contains 117 slides and 29 PDF pages. Original slides and readings remain in the student's supplied archive; they are not bundled here. The wiki paraphrases them and includes newly written examples. Three short Python source files are inventoried and explained, rather than copied into this repository.

**Provenance convention:** each chapter identifies its course sources. Worked examples, pseudocode, extra formulas, and qualifications labeled **Study supplement** are explanatory additions, not claims that the instructor supplied that exact example. Coverage of probability, Bayes, Markov models, planning, and ethics is limited to mentions in the uploaded material; these are not presented as completed lecture units.

## How to study

Read agents before search. Practice tracing a frontier, backing up minimax values, binding Prolog variables, and computing one optimizer update. Use the comparison guide to explain *why* an algorithm fits a problem. Finish with the practice questions without looking at the answers.

## AI assistance disclosure

This wiki was drafted with AI assistance from the provided class materials, with source mapping, arithmetic checks, and local-link validation. The student should review it against class discussions and disclose their own contributions as required by the instructor. It is a study resource, not a submission of the separate Prolog lab.

## Repository layout

```text
README.md
SOURCE_INVENTORY.md
REFERENCES.md
GITHUB_SHARING.md
CONTRIBUTING.md
wiki/                         # linked study chapters
```

No software installation is needed to read the wiki. GitHub renders the Markdown tables, code blocks, and LaTeX formulas. Upload the **contents of this folder**, so this README appears at the repository root.
