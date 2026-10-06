# Logic, inference, and Prolog

[Home](../README.md) · [Next: optimization](07-optimization.md)

**Course source:** `XX_Logic Programming with Prolog.pptx`, slides 2–31. This chapter summarizes the substantial Prolog unit, including its examples and lab instructions.

## Contents

- [Logic and Horn clauses](#logic-and-horn-clauses)
- [Chaining and resolution](#chaining-and-resolution)
- [Terms, facts, rules, and queries](#terms-facts-rules-and-queries)
- [Unification and execution](#unification-and-execution)
- [Arithmetic and lists](#arithmetic-and-lists)
- [Recursion and data structures](#recursion-and-data-structures)
- [Negation and control](#negation-and-control)
- [Answer collection and debugging](#answer-collection-and-debugging)
- [Lab 01 checklist](#lab-01-checklist)

## Logic and Horn clauses

A proposition is true or false. Propositional logic combines symbols with negation, conjunction, disjunction, and implication. First-order logic adds objects, predicates, variables, and quantifiers.

**Study supplement: compact truth table.**

| P | Q | not P | P and Q | P or Q | P implies Q |
|---|---|---|---|---|---|
| true | true | false | true | true | true |
| true | false | false | false | true | false |
| false | true | true | false | true | true |
| false | false | true | false | false | true |

A **literal** is a positive or negated atom. A **clause** is a disjunction of literals. CNF is a conjunction of clauses. Propositional formulas can be rewritten equivalently into CNF, although direct expansion can increase size.

A Horn clause has at most one positive literal. A definite clause has exactly one:

$$\neg A\lor\neg B\lor C\quad\equiv\quad A\land B\Rightarrow C.$$

A fact has an empty body. A clause with no positive literal is a goal clause. `P or Q` with two positive literals is not a Horn clause. This restriction improves tractability but limits expressiveness.

Propositional definite-clause entailment can be computed in linear time in KB size with an appropriate chaining algorithm. This bound does **not** apply to arbitrary first-order Prolog programs. General first-order entailment is semidecidable.

## Chaining and resolution

Forward chaining starts with facts and derives consequences. Backward chaining starts with a query and seeks facts/rules supporting it. Prolog uses backward reasoning operationally.

**Study supplement:** from `human(socrates)` and `human(X) -> mortal(X)`, forward chaining derives `mortal(socrates)`. Backward chaining for `mortal(socrates)` reduces it to proving `human(socrates)`.

Resolution combines complementary literals to derive a consequence. To prove a query by refutation, add its negation and derive contradiction. Prolog's SLD resolution specializes resolution to definite clauses and selected goals.

“Algorithm = Logic + Control” separates the intended relations from the strategy used to search for proofs. The logic alone does not guarantee that a particular Prolog search order terminates.

## Terms, facts, rules, and queries

| Item | Example | Meaning |
|---|---|---|
| Atom | `ana`, `'Ana María'` | Named constant |
| Variable | `X`, `Who`, `_` | Starts uppercase or underscore |
| Number | `42`, `3.14` | Numeric term |
| Compound term | `parent(hector, ana)` | Functor plus arguments |
| Fact | `parent(hector, ana).` | Relationship asserted |
| Rule | `father(X,Y) :- parent(X,Y), male(X).` | Head follows from body |
| Query | `?- father(hector, Who).` | Ask for successful substitutions |

`father/2` means predicate `father` with two arguments and differs from `father/3`. Every clause and query ends with a period. Comma is conjunction, semicolon offers alternatives, and `:-` reads “if.” Clause variables are implicitly universally quantified; query variables ask for witnesses/substitutions.

The deck's family example uses parent facts and defines grandparents, siblings, and ancestors. A small related study example is:

```prolog
parent(hector, ana).
parent(hector, luis).
parent(ana, sofia).

grandparent(X, Z) :- parent(X, Y), parent(Y, Z).
sibling(X, Y) :- parent(P, X), parent(P, Y), X \= Y.
ancestor(X, Y) :- parent(X, Y).
ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).
```

`grandparent(hector, sofia)` succeeds. `sibling(ana, ana)` fails. Recording two shared parents can give two proofs of a sibling relationship, so duplicate answers need attention.

## Unification and execution

Unification finds substitutions that make terms identical. It does not evaluate arithmetic.

```prolog
?- f(a, Y) = f(X, b).
X = a, Y = b.

?- [H|T] = [1,2,3].
H = 1, T = [2,3].

?- f(a) = g(a).
false.
```

Compound terms require matching functors and arities, then pairwise unification of arguments. In the ordinary SWI behavior described in the lecture, `X = f(X)` can construct a cyclic term. `unify_with_occurs_check(X, f(X))` fails instead.

Prolog selects the leftmost goal, tries matching clauses in file order, substitutes the clause body, and continues. On failure it backtracks, undoing bindings and trying alternatives. Press `;` for another answer.

The lecture's path example shows that left recursion can loop even when a proof exists. SLD's proof system and the interpreter's depth-first scheduling must be distinguished. Reordering clauses can help a particular query but is not a general termination proof. Tabling memoizes calls/answers and can resolve suitable recursive cycles; it does not guarantee termination of every program with an unbounded space of distinct terms.

## Arithmetic and lists

| Operator | Purpose |
|---|---|
| `=` | Unification |
| `is` | Evaluate the right expression, then unify the result |
| `=:=` / `=\=` | Numeric equality / inequality after evaluation |
| `==` | Term identity without binding |
| `\=` | Terms are currently not unifiable |
| `<`, `>`, `=<`, `>=` | Arithmetic comparisons |

`X = 3+4` binds X to an expression term. `X is 3+4` binds X to 7. `3+4 = 7` fails; `3+4 =:= 7` succeeds. `X is Y+1` raises an instantiation error if Y is unbound.

A list is `[]` or `[Head|Tail]`. `[1,2,3]` abbreviates `[1|[2|[3|[]]]]`. The lecture implements membership, concatenation, and length recursively:

```prolog
mymember(X, [X|_]).
mymember(X, [_|T]) :- mymember(X, T).

myappend([], L, L).
myappend([H|T], L, [H|R]) :- myappend(T, L, R).
```

`append(X,Y,[1,2,3])` can enumerate four splits because it describes a relation. By contrast, ordinary `is/2` arithmetic is directional. Not every predicate works equally well in every input/output mode.

## Recursion and data structures

Factorial uses a base fact `factorial(0,1)` and a recursive clause for positive N. Compute `N1 is N-1` before recursing; multiply after the result returns. Querying `factorial(X,120)` with the lecture's arithmetic version fails operationally with an instantiation error, rather than searching backward for X.

The lecture's Fibonacci sequence uses **F(0)=1, F(1)=1**, giving F(10)=89. Naive branching recursion repeats subproblems and has exponential growth. An accumulator version runs in linear iterations, while tabling also avoids repeated proof work. Do not substitute the alternative textbook seed F(0)=0 without noting the change.

Mutually recursive even/odd predicates determine list-length parity without inspecting elements. Returning atoms `true`/`false` is different from succeeding or failing; the latter is idiomatic for a yes/no relation. Replace unused singleton variables with `_`.

The deck's `isPerm` example checks mutual membership, which is set equality rather than permutation equality. `[1,1,2]` and `[1,2,2]` have the same set but different multiplicities. A grounded-list check using `msort(X,S), msort(Y,S)` preserves duplicates.

A binary search tree can be represented as `empty` or `node(Key,Left,Right)`. Pattern matching selects branches. Insertion relates an old immutable term to a new one. The shown version has no equal-key clause, so inserting an already present key fails unless an explicit duplicate policy is added.

For N-queens, select unused columns and test diagonal safety during construction. [The CSP chapter](05-csp.md#n-queens) explains the mathematical representation. The lecture's accumulator constructs the safe list by prepending; row order is effectively reversed, which preserves non-attacking validity by reflection.

## Negation and control

`\+ Goal` succeeds when the interpreter cannot prove Goal. This is **negation as failure** under a closed-world reading, not classical negation with an open-ended world.

Bind relevant query variables before negating. `\+ parent(X,ana)` does not enumerate non-parents: it fails if any parent of Ana can be proved. `X=sofia, \+ parent(X,_)` asks whether Sofia has no child recorded.

The cut `!` commits to choices already made in the current predicate invocation, discarding alternatives that could otherwise be tried. It can change answers, not merely speed.

The slide's faulty maximum rule can incorrectly let `max(5,3,3)` succeed because the first head fails to unify before its cut executes. The corrected form delays output binding:

```prolog
max_value(X, Y, M) :-
    ( X >= Y -> M = X ; M = Y ).
```

This assumes X and Y are numeric and bound. Control constructs still have procedural behavior.

## Answer collection and debugging

| Predicate | Use |
|---|---|
| `findall(T,G,L)` | Collect answers in proof order, preserving duplicates; [] for no answers |
| `setof(T,G,L)` | Sorted unique answers; fails for none; free variables can group answers |
| `bagof/3` | Grouped collection without deduplication |
| `Var^Goal` | Existentially quantify a variable inside bagof/setof |
| `aggregate_all(count,G,N)` | Count solutions without retaining a full answer list |
| `between/3`, `select/3`, `permutation/2` | Generate alternatives |
| `sort/2`, `msort/2` | Sort with / without duplicate removal |
| `trace`, `notrace` | Enable / disable the Call, Exit, Redo, Fail debugger |
| `listing/1`, `make/0` | Inspect predicates / reload changed files |

Common mistakes are a missing period, uppercase names intended as atoms, `=` where evaluation was intended, singleton warnings, left recursion, and negation before binding.

## Lab 01 checklist

The uploaded assignment requires:

1. At least 16 people across four generations, `spouse/2`, both parents recorded for each child, a couple with at least three children, and a person with none (20 points).
2. At least eight relationship rules, including the listed mother, sister, grandmother, uncle, cousin, father-in-law relations, plus an original recursive relation other than ancestor (35 points).
3. At least 20 `plunit` tests, six negative, including no self-sibling; all must pass (25 points).
4. Half-page analysis of self-sibling exclusion, duplicate proofs, and the closed-world assumption (20 points).
5. Optional terminating `related/2` over parent, child, and marriage links (+10).

Deliverables are `lastname_firstname_lab01.pl` and a PDF of at most two pages containing test output and analysis. The slide requests a clean load without errors or singleton warnings and disclosure of AI help. The referenced `01_Code/` folder and its files are **not included** in this ZIP. This wiki explains the assignment; it does not claim to contain those original files or a completed lab.
