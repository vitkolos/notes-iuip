# Exam

## Foundations

- Define a constraint satisfaction problem (including the notion of constraint) and its solution.
- Define Boolean CSP and Binary CSP and show transformations of CSP to Binary CSP (dual encoding, hidden variable encoding).

## Local search techniques

- Explain the core principles and notions of local search, including intensification and diversification, (non)strict local/global optimum, plateau.
- Describe hill climbing, min-conflicts, and random walk techniques and discuss their relations.
- Describe Tabu Search, GSAT, Genet, and simulated annealing and discus their properties.

## Look-back search techniques

- Describe backtracking as a CSP solving technique, discuss its weaknesses (thrashing, redundant work, late detection of conflicts).
- Describe backjumping and its versions (graph-directed, Gaschnig), discuss how to find a conflicting variable.
- Describe dynamic backtracking and its core components.
- Describe backmarking.

## Consistency techniques

- Define Node Consistency and describe how it can be achieved.
- Define Arc Consistency and describe and compare algorithms to achieve it (AC-1, AC-2, AC-3, AC-4, AC-3.1), Discuss their time complexities.
- Define Directional Arc Consistency, compare it with AC (discuss tree-structured CSPs), and describe how it can be achieved.
- Define Path Consistency and describe algorithms to achieve it (PC-1, PC-2 in detail, other in principle), define direction path consistency.
- Describe relations between AC and PC, explain restricted path consistency algorithm.
- Define the concepts of (strong) k-consistency and (i,j)-consistency and their relation to backtrack-free search.
- Explain inverse and singleton consistencies.

## Higher-arity constraints

- Define Generalized Arc Consistency and describe how it be achieved.
- Define global constraints and describe their relation to GAC, give some examples of global constraints including the filtering algorithm (all-diVerent, gcc, lex, regular, grammar, slide, unary resources).

## Consistency techniques in search

- Describe integration of consistency techniques and search.
- Describe and compare forward checking, partial look-ahead, and full look-ahead.
- Describe variable-ordering and value ordering heuristics, explain fail-first and succeed-first principles.
- Describe various branching schemas (enumeration, step labeling, bisection).
- Explain cycle-cutset technique and MAC Extended algorithm.

## Incomplete and discrepancy search techniques

- Explain the principle of incomplete depth-first search.
- Describe algorithms bounded backtrack, iterative broadening, depth-bounded, and credit search.
- Explain principles of discrepancy search, describe Limited Discrepancy Search, Improved LDS, and Depth-Bounded Discrepancy Search.

## Constraint Optimization

- Define a constraint optimization problem, including the representation of objective function.
- Describe branch-and-bound technique and its versions.

## Over-constrained problems

- Define an over-constrained problem.
- Describe techniques Partial CSP, Valued CSP, and Semiring-based CSP and their instances.
- Define constraint hierarchies, including comparators (local/global, predicate/metric) and describe techniques to solve them (DeltaStar, DeltaBlue, Indigo, projection).
