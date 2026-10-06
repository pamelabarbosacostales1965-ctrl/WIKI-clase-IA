# References, provenance, and corrections

[Home](README.md)

## Course sources

The [inventory](SOURCE_INVENTORY.md) identifies all original filenames and checksums. Slide numbers are one-based slide order. PDF page numbers are one-based positions in the supplied file; printed pagination differs.

| Topic | Source locator |
|---|---|
| Instructor, syllabus, assessment context | Instructor Introduction, slides 1–5 |
| Intelligence, computing history, Turing, Dartmouth | Introduction to AI, slides 2–9 |
| Models, backpropagation, SVM, deep learning, causality | Introduction to AI, slides 10–15 |
| Antikythera and Talos | Introduction to AI, slides 17–19 |
| Problem components and repeated states | Problem Solving, slides 2–5 |
| BFS, DFS, greedy, A*, heuristic properties | Problem Solving, slides 6–16 |
| Minimax and alpha–beta | Problem Solving, slides 17–22 |
| CSP | Problem Solving, slides 23–25 |
| Agent function, rationality, PEAS | Intelligent Agents, slides 2–7 |
| Environment types and agent designs | Intelligent Agents, slides 8–18 |
| CNF, Horn, chaining, language origins | Prolog, slides 2–10 |
| Syntax, unification, proof search, arithmetic | Prolog, slides 11–16 |
| Recursion, lists, examples, negation/cut | Prolog, slides 17–23 |
| Built-ins, queens, debugging, lab | Prolog, slides 24–31 |
| Evolutionary computation and GA | Optimization, slides 2–7; Holland PDF pages 2–8 |
| PSO | Optimization, slides 8–11; Kennedy/Eberhart PDF pages 1–7 |
| ACO | Optimization, slides 12–15; Dorigo et al. PDF pages 1–13 |
| ABC | Optimization, slides 16–19 |
| GD and SA | Three uploaded Python files |

Readings: Holland, J. H. (1992), “Genetic Algorithms,” *Scientific American*, 267(1), 66–73 (the upload includes a JSTOR cover and an advertisement); Kennedy, J., and Eberhart, R. (1995), “Particle Swarm Optimization,” proceedings paper, printed pages 1942–1948; Dorigo, M., Maniezzo, V., and Colorni, A. (1996), “Ant System: Optimization by a Colony of Cooperating Agents,” *IEEE Transactions on Systems, Man, and Cybernetics—Part B*, 26(1), 29–41.

The Prolog slides recommend Russell & Norvig, Luger, Bratko, and Sterling & Shapiro. Those books are **recommended by the course** but were not uploaded or independently read for this wiki.

## Corrections and qualifications

| Source issue | Treatment in this wiki |
|---|---|
| Introduction slide 9 calls Prolog a language created by Dennis Ritchie and describes imperative features | Use Prolog deck slide 8: Colmerauer/Roussel, Marseille, 1972, with Kowalski's logical foundations. The Ritchie description is mixed-in C content |
| Agents slide 2 begins with proposition definitions | Define agent from the sensor/actuator examples and surrounding agent material |
| Search slides simplify completeness and duplicate control | Add finite-space, branching, cost, consistency, and reopening qualifications |
| DFS memory bound versus explored set | Distinguish tree traversal memory from graph duplicate storage |
| Alpha–beta “optimal complexity” | Identify it as the ideal-ordering bound, not the worst case |
| “Cheap” Horn inference | Restrict linear entailment claim to propositional definite-clause KBs |
| Tabling fixes example loops | Explain it is not a termination guarantee for all programs |
| ABC and other historical year labels | Avoid treating lecture year labels as verified first-invention dates |
| `gd_steroids.py` objective/surface mismatch | Explain `(y+2)^2` versus `(y+1)^2`; provide suggested corrections |
| SA very fast cooling and underflow | Explain positive-temperature safeguards and schedule design |
| ACO rho notation differs between slides and paper | Label evaporation versus retention conventions explicitly |
| Prolog slides refer to `01_Code/` | Mark missing; do not claim the folder was included |
| Slide lab says “Due today” | Do not infer a calendar deadline |

Some historical dates and simplified claims in the introduction may deserve verification against primary historical sources. This study wiki prioritizes the supported concepts and does not silently certify every timeline detail.

## Inspection method and limits

All ZIP entries were inventoried; all 117 slide XML text layers and all 29 PDF text layers were extracted for review. Embedded image figures on text-light slides were also inspected, including search traces, heuristic conditions, minimax trees, and optimizer pseudocode/formulas. Extraction of scanned/embedded equations can lose notation, so the wiki uses explanatory formulas with their conventions stated rather than pretending every formula was text-extractable. Original media, lecture videos, classroom discussion, and any absent course resources are outside the source set.

The repository contains paraphrased study explanations, not complete copies of the published readings or instructor slides. No redistribution license for the course sources was supplied, so no open-source license is assigned to those originals.

The only external web source used for operational instructions was [GitHub's collaborator invitation documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository), checked October 1, 2026. It is not used as AI course evidence.
