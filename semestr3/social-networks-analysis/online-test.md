# Online Test

## Introduction

- six degrees of separation
	- an experiment on the small-worlds phenomenon
	- random people from Nebraska were asked to send a letter (via intermediaries) to a stock-broker in Boston
	- could only send to someone whom they knew on a first-name basis
	- among the letters that found the target, the average number of links was six
- scale-free (SF) networks
	- some nodes (“hubs”) have extremely many connections to other nodes
	- most nodes have just a few connections to other nodes
	- resilient to a random disturbance, vulnerable to coordinated attacks
	- examples
		- social networks: scientific collaboration (researchers co-authoring papers), Hollywood (actors starring in the same movie)
		- biological networks: cell metabolism, protein regulatory networks
		- internet, WWW
	- two main mechanisms
		- growth
		- preferential attachment (“the rich get richer”)
- practical applications
	- marketing campaigns based on social networking
	- law enforcement
	- detection of conflicts of interest
	- prevention of contagious diseases
	- optimization of the structure and capacity of communication networks

## Basic Concepts

- network representations
	- directed × undirected graph
	- edge list × adjacency matrix
	- ego network
	- weighted edges → tie strength
		- homophily = tendency to relate to people with similar characteristics
		- transitivity
			- strong ties are often transitive
			- transitivity and homophily lead to the formation of cliques
		- bridges = nodes and edges that connect different groups
			- usually weak ties
- shortest path algorithms
	- single source: Dijkstra, Bellman-Ford (allows negative edge weights)
	- all pairs: Dijkstra, Floyd-Warshall (allow negative edge weights), Johnson (allow negative edge weights, better for sparser graphs)
- key players (how to identify them)
	- degree centrality
		- number of edges incident with the node
	- betweenness centrality
		- number of shortest paths passing through a node divided by all shortest paths in the network
			- for a given node $v$, calculate the number of shortest paths between nodes $i$ and $j$ that pass through $v$, and divide by all shortest paths between nodes $i$ and $j$
			- sum the computed values for all node pairs $i, j$
			- sometimes normalized such that the highest value is 1
		- indicates nodes that are on “communication paths”
			- helps to determine points where the network might break apart
	- closeness centrality
		- the reciprocal of the mean length of shortest paths from a node to all other nodes in the network (1 ÷ average number of hops needed to reach some other node)
		- measure of reach
		- useful when the speed of dissemination is of main concern
	- eigenvector centrality
		- proportional to the sum of eigenvector centralities of all nodes directly connected to the considered node
		- a node with a high eigenvector centrality is connected to other nodes with a high eigenvector centrality
		- similar to PageRank
		- useful in determining who is connected to the most connected nodes
	- sometimes, it's more useful to identify sets of key players (not only individual key players)
- structural equivalence
	- two actors are structurally equivalent if their positions can be swapped without modifying the overall structure of the network (~ they have the same neighbors)
	- approximate structural equivalence can be used for hierarchical clustering of social networks
- cohesion (reciprocity, density, clustering)
	- cohesion = how to characterize a network's structure
	- reciprocity
		- ratio of the number of relations that are reciprocated (there is an edge in both directions)
			- reciprocated relations ÷ all relations
			- two vertices are said to be related if there is at least one edge between them
			- makes sense only in directed graphs
		- degree of mutuality / reciprocal exchange in networks (related to social cohesion)
	- density
		- number of edges ÷ total number of possible edges
		- total number of possible edges
			- $\frac{n(n-1)}2$ for an undirected graph
			- $n(n-1)$ for a directed graph
		- a clique has density equal to one
	- clustering
		- indicates the presence of communities
		- node's clustering coefficient $C(i)$ measures the *density* of its neighborhood $N(i)$
		- $N(i)$ … network consisting only of the nodes directly connected to $i$
		- network clustering coefficient $C$ is the average of the individual coefficients of its nodes
- network's diameter
	- consider the lengths of shortest paths between any two nodes in a network, take the maximum
	- indicates how long it will take at most to reach any node in the network
- a small world
	- network that looks almost random but exhibits a significantly high clustering coefficient and a relatively short average path length
	- → nodes cluster locally and can be reached in a few steps
	- very common in social networks because of transitivity in strong social ties and the ability of weak ties to reach across clusters
	- *small world* networks have many clusters but also many bridges between the clusters that help shorten the average distance between nodes
	- → six degrees of separation
- social connections – strong and weak ties
	- users might have thousands of friends online, but not every friendship is the same (there may be stronger and weaker ties)
	- how to estimate the strength of ties?
		- analyze network topology – look for bridges (→ weak ties)
			- we may need to relax the definition – removing the bridge increases the distance (the larger the distance, the weaker the tie)
		- neighborhood overlap
			- the larger the overlap, the stronger is the tie
			- overlap = $\frac{|N_i\cap N_j|}{|N_i\cup N_j|-2}$
				- −2 to exclude $i,j$
		- learn from profiles and interactions
			- we can use maximum likelihood estimation
		- learn from user activities
			- we can learn how the users influence their friends if the user activity log is accessible (→ influence modeling, LTM / ICM)

## Influence Modeling

- common properties of influence modeling methods
- linear threshold model (LTM)
- independent cascade model (ICM)
- influence maximization
- correlation

## Homophily, Social Influence, Affiliation

- homophily, triadic closure
- selection and social influence
- affiliation networks
- Schelling's model of segregation
- positive and negative relationships

## Link Analysis

- statistical measures
- hubs and authorities (HITS)
- PageRank
