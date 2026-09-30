# Lecture

- discord
- https://sites.google.com/view/agtg-101
- no regular exercise classes
- homework almost every week
	- one strict deadline for the first batch
- exams: going through the homework together
	- do we understand it?
	- does it do what it's supposed to do?

## Normal-Form Games

- simultaneous decision making
- each players chooses their strategy, all players execute them simultaneously
- $\braket{\mathcal N, (\mathcal A_i), (u_i)}$ … players, actions, utility (payoff)
- payoff maps all the performed actions to $\mathbb R$
- if we consider only two players, we can describe the game using a matrix
- constant-sum game … $u_1+u_2=c$ in all cells
	- if $c=0$, it's a zero-sum game ($u_1=-u_2$)
- strategies: pure × mixed
	- strategy $\pi_i$
	- strategy profile $\pi=(\pi_1,\dots,\pi_N)$
	- $\pi_{-i}$ … strategies of all players in $\pi$ except $\pi_i$
	- support of strategy $\pi_i$ … set of all actions with non-zero probability
- we can compute expected utility
- best response $b(\pi_{-i})$
	- set of strategies that maximize utility for given $\pi_{-i}$
- best response condition
	- for any best response strategy $\pi_i$, all actions in its support have the same expected utility
	- (otherwise, we could move all the mass to the “best” one)
- set of best responses is convex
	- any convex combination of BRs is also BR
- BRV (best response value)
- dominated strategies
	- iterated removal of dominated strategies
- homework
	1. strategy profile evaluation (what is the expected utility?)
	2. best response calculation
	3. iterated removal of dominated strategies
