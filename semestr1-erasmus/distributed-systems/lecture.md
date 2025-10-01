# Lecture

- multi-core processor
	- is it a distributed system? no
	- the whole processor crashes (we cannot have one core working and other one crashed)
- partial failure
	- in a distributed system, the components may fail independently
	- „distribuovaný systém je to tehdy, když můj počítač přestane fungovat, protože se rozbil počítač, o kterém jsem ani nevěděl, že existuje“
- sharing information, taking a common decision
- why do we want/have a distributed system?
	- users are in different places → it is a distributed system by nature
	- better performance, stability (if one server fails, we have another)

## Ordering of Events

- notation
	- set of processes $P=\set{p_1,\dots,p_n}$
	- they communicate through channels (channel from $p_i$ to $p_j$ … $C_{ij}$)
	- event $\# k$ on process $p_i$ … $e_i^k$
		- event changes the state of the process
	- states of the process $\sigma_i^0,\sigma_i^1,\dots$
		- event $e_i^1$ performs the transition from $\sigma^0_i$ to $\sigma_i^1$ on process $p_i$
	- local history $h_i=e^1_i e^2_i e^3_i \dots$
	- global history $H=h_1\cup h_2\cup h_3\dots$
- happened_before ($\to$) relation between two events
	- first case: $e_i^k\to e_i^\ell$ iff $k\lt\ell$
	- second case: send($m$) $\to$ recv($m$)
		- we can receive a message $m$ only after we send it
	- transitivity: $e\to e'\land e'\to e''\implies e\to e''$
	- antisymmetry: $e\to e'\implies e'\not\to e$
	- it is a partial ordering of events
	- if there is no relation between $e$ and $e'$, we say they are concurrent
		- $e||e'$
- global state $(\sigma_1^{k_1},\sigma_2^{k_2},\sigma_3^{k_3},\dots)$
	- global state is composed of the local state of every process
- cut
	- cut $C$ … subset of the global history $H$ that includes a prefix of each local history
	- consistent cut … the global state could have existed
		- cut $C$ is consistent iff $e'\in C\land e\to e'\implies e\in C$
- Chandy-Lamport
	- we assume FIFO channels
	- to save a snapshot, we need an initiator process which is the first to save its state and broadcast the message SNAPSHOT
	- when process $p_i$ receives the SNAPSHOT message, it saves its state and also broadcasts SNAPSHOT (there are no other events in between)
	- the state of channel $c_{ji}$ corresponds to the messages that the process $p_i$ received from $p_j$ between broadcasting SNAPSHOT and receiving SNAPSHOT from $c_j$
	- after $p_i$ receives SNAPSHOT from all processes, it knows that the computation of the snapshot is terminated

## Time

- how to put timestamps on events to have guarantees that one event happened before another event?
	- I would like a timestamp function $TS$ such that $e\to e'\iff TS(e)\lt TS(e')$
	- we are assuming an asynchronous system
		- no bound on message delays
		- no bound on relative speed of processes
- Lamport Clock $LC$
	- algorithm
		- initial state … $LC_i\leftarrow 0$
		- for any internal event … $LC_i\leftarrow LC_i+1$
		- on $\mathrm{send}(m)$ … $LC_i\leftarrow LC_i+1$
			- + attach $LC_i$ to $m$, so that $ts(m)=LC_i(\mathrm{send}(m))$
		- when $p_j$ receives $m$
			- $LC_j\leftarrow\max(LC_j,ts(m))+1$
	- what can we say about LC?
		- $e\to e'\implies LC(e)\lt LC(e')$
			- we don't have $\impliedby$
		- $LC_i(e)$ corresponds to the length of the longest chain of events leading to $e$
- vector clocks
	- definition
		- for $i=j:VC(e_i)[j]=$ number of events on $p_i$ up to and including $e_i$
		- for $i\neq j:VC(e_i)[j]=$ number of events on $p_j$ that happened_before $e_i$
	- algorithm
		- if $e_i$ is internal or $\mathrm{send}(m)$
			- $VC(e_i)[i]\leftarrow VC_i[i]+1$
			- $VC(e_i)[j]\leftarrow VC_i[j]$
		- if $e_i$ is $\mathrm{recv}(m)$
			- $VC(e_i)\leftarrow\max(VC_i,ts(m))$
			- $VC(e_i)[i]\leftarrow VC(e_i)[i]+1$
