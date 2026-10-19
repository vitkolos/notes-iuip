# Lecture

- problem
	- variables
	- domains
	- constraints
- a feasible solution = a complete consistent assignment of values to variables
- an optimal solution = a feasible solution that minimizes/maximizes a value of some objective function
- properties of constraints
	- they express partial information
	- they provide a local view of the problem – connect only a few variables
	- can be heterogeneous (domains can be different; they don't have to be linear constraints)
	- are non-directional (left-hand side and right-hand side have no special meaning)
	- are declarative (they don't tell you how to satisfy them)
	- are additive (their order is not important; we care about their conjunction)
	- are rarely independent (they share variables)
- advantages of CP
	- close to real-life problems
	- declarative manner (we can focus on problem description without paying too much attention to problem solving)
	- co-operative problem solving (we can integrate various solving approaches – Gaussian elimination for linear inequalities, bipartite graph matching for combinatorial constraints, …)
	- semantic foundation (we can use clean and elegant modelling languages)
- limitations of CP
	- efficiency (combinatorial explosion, many problems are NP-complete)
	- hard-to-predict behaviour (it's hard to estimate the efficiency before running the model on real data)
	- model stability (new data = new problem)
	- too local (individual constraints give a very limited insight – one constraint may look satisfiable even though the whole model is not)
	- weak co-operation of solvers (usually done only through sharing variables)
- binary CSP
	- CSP where all the constraints are binary
	- note: unary constraints can be encoded into domains directly
	- dual encoding: k-ary constraint can be converted to a dual variable with the domain consisting of compatile tuples

---

generate and test, local search

---

- chronological backtracking
	- let's assign the variables one-by-one and check if the partial assignment is consistent
	- problems
		- we throw away the reason of the conflict (“thrashing”)
			- solution: backjumping (jump to the source of the failure)
		- redundant work – unnecessary constraint checks are repeated
			- solution: backmarking, backchecking
		- late detection of the conflict
			- causes the problems above
			- solution: forward checking
	- two kind of solutions: look back × look ahead
- backjumping
	- identify the source of the conflict → jump there
	- graph-directed backjumping
		- we jump as little as possible so that we don't skip any consistent assignments
		- we keep a list of variables that could have caused the conflict – we always jump to the last one
	- Gaschnig backjumping
		- N queens: pro každou možnou hodnotu proměnné určíme, s jakými proměnnými vznikne konflikt (zajímá nás jen ta „nejmenší“, tedy nejvzdálenější) → skočíme na tu „největší“ (tzn. nejbližší) z nejmenších
		- where there's multiple variables participating in one constraint, we are interested in the last one that was assigned
		- takže na číslech proměnných spočítáme postupně maximum (přes proměnné), minimum (přes podmínky) a maximum (přes hodnoty) → získáme číslo proměnné, kam je potřeba skočit
		- ale můžeme skočit jenom jednou, pak musíme klasicky backtrackovat
	- conflict-driven backjumping
		- Gaschnig with multiple jumps
		- we keep a conflict set of variables
- dynamic backtracking
	- when jumping back, the in-between assignment is lost
	- instead of backjumping, we can reorder the variables
	- and we remember the source of conflict
- backmarking
	- memorizes results of tests so that we don't need to do redundant work