# Lecture

- best channel to convey information = vision
	- highest bandwidth of all the senses
	- extends memory and cognition – we use drawings to “think more clearly”
	- people think visually
- pre-attentive perception
	- the time to find the blue dot is constant – no matter the total number of dots
		- assuming we can distinguish the colors
- Anscombe's Quartet – four datasets with the same statistical properties
- when computing average, we assume that it represents the underlying distribution well
- information visualization = use of computer-supported, interactive visual representations of data to amplify cognition
- scientific visualization – the datasets have a given spatialisation (the coordinates already exist), continuous
- data visualization – web-based, communication
- challenges: diversity, scale
- visual information-seeking mantra
	- overview first
	- zoom and filter
	- details on demand
- visual perception is a two stage process
	- parallel extraction of low-level properties
	- sequential goal-directed processing
- retina performs parallel processing of different attributes
- brain performs sequential processing (object segmentation, identification)
- readings: [Graphs in Statistical Analysis](http://iihm.imag.fr/blanch/teaching/infovis/readings/1973-Anscombe-Graphs_in_Stats.pdf) & [The Eyes Have It](http://iihm.imag.fr/blanch/teaching/infovis/readings/1996-Shneiderman-Mantra.pdf); viewing: [Hans Rosling’s TED talks](https://www.ted.com/speakers/hans_rosling)
- density of receptors decreases with the distance from the center of vision (so the peripheral vision is not that sharp)
- peripheral vision is mostly colorblind
- http://xkcd.com/1080/
- Gestalt psychology
	- one stimulus, two perceptions
	- there is a difference between stimulus and perception
	- emergence – we need to see the whole picture, not just parts
	- reification – perception contains more spatial information than the stimulus
	- multistability – ambiguous stimuli can generate different perceptions but they cannot coexist simultaneously
	- invariance – objects are recognized independently of various variations (transformations, lightning, …)
	- laws of grouping – law level perceptions are grouped into higher-level objects
		- good Gestalt
- information visualization pipeline
	- source data → data tables
		- data transformations
	- data tables → visual abstraction
		- visual mappings
		- transition from data form to visual form
		- we use data attributes to create (visual) marks
	- visual abstraction → views
		- view transformations
		- result … actual pixels
- example: gapminder (data attributes → visual channels)
	- income → x
	- life expectancy → y
	- country → details on demand
	- population → size
	- region → color
- interactions
	- the user can manipulate 1) data transformations, 2) visual mappings, 3) view transformations
	- zoom … view transformation
	- filtering … data transformation
	- in gapminder, we can also edit visual mappings
- taxonomies of data types
	- “what comparisons can I make?”
	- “how can I aggregate the data?”
	- nominal … only equality (=)
		- aggregation … mode (we show the most frequent one) or top-k
			- if we have a taxonomy (hierarchy), we can group the data
	- ordered … ordering and equality (<, =)
		- aggregation … median, quantiles, histogram (count per bucket)
	- quantitative … “how much smaller is it?”
		- → intervals … $v-v'$
		- → ratios … $v/v'$
			- only if there is a meaningful zero on the scale
		- aggregation … mean, std dev, skew

## Visual Mapping

- how to map between attributes and visual channels
- properties of visual channels
	- association $(\equiv)$
		- does the visual channel play well with the other visual channels?
		- size does not provide association – the other visual variables are more difficult to see for smaller sizes
	- selection $(\neq)$
		- can you focus on a specific subset in this visual channel?
		- color provides selection
	- order $(O)$
		- items can be ordered according to this variable, without relying on a lookup to a legend
	- quantity $(Q)$
		- the difference between two items can be quantified
- channels
	- position $(\equiv,\neq,O,Q)$
	- size $(\neq,O,Q)$
		- beware: for quantity judgement, our perception is biased
			- Stevens' Law: $\frac{p(x_1)}{p(x_0)}=\left(\frac{x_1}{x_0}\right)^\beta$
			- $p$ … perception
			- $\beta$ is different for length, area, and volume
			- in 2D, we underestimate large sizes (in 3D it's even worse)
		- note on depth
			- depth is perceived mainly because it impacts size
			- using the third dimension introduces ambiguity: is it small or is it far away?
			- but we can keep all the objects the same size and only apply motion parallax & skew instead of perspective
	- value $(\neq,O)$
		- lightness of color
		- light marks are harder to see
	- texture $(\equiv,\neq,O)$
		- usually black and white (dark and light color) – we can mix it with color channel
		- probably underused
	- color $(\equiv,\neq)$
		- we don't perceive the axis of wavelengths
		- colors are usually used as labels
	- orientation $(\equiv,\neq)$
		- only for some shapes (not circles)
	- shape $(\equiv)$
		- does not provide selection → it's better to use color for grouping
- Mackinlay: suitability of variables, possible combinations
	- distinguishes more visual channels
	- ordered lists – the best channels on top
	- systematic approach to choosing visual channels
- position is the best visual channel
- example: gapminder
	- attribute, data type (N/O/Q), X Y Z T R, CP
	- life expectancy Q, Y→P (0D)
	- income per capita Q, X→P
	- country N, CP (label)
	- population Q, R→S (size)
	- region N, R→C (color)
- time (T) … animation
- dimensions
	- P … 0D
	- L … 1D
	- A … 2D
- filtering (F)
	- slider … select one level
	- br … bounded range
- animated gapminder
	- extra attribute: year Q,  F→sl\>, T

*table for the Napoleon's chart*

| Variable  | D     | X   | Y   | Z   | T   | R   | —   | \[] | CP  |
| --------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| Number    | Q     |     |     |     |     | S   |     |     |     |
| Direction | N     |     |     |     |     | C   |     |     |     |
| Town      | N     |     |     |     |     |     |     |     | tx  |
| Lon.      | QXlon | L   |     |     |     |     |     |     |     |
| Lat.      | QYlat |     | L   |     |     |     |     |     |     |
| Date      | Q     |     |     |     |     |     |     |     | tx  |
| Temp.     | Q     |     | P   |     |     |     | L   |     | tx  |

*in-class solution*

| Attributes | D   | X   | Y   | Z   | T   | R   | —   | \[] | CP   |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
| # men      | Q   |     |     |     |     | S   |     |     | text |
| location   |     |     |     |     |     |     |     |     |      |
| → long.    | Q   | L   |     |     |     |     |     |     |      |
| → lat.     | Q   |     | L   |     |     |     |     |     |      |
| cities     | N   |     |     |     |     |     |     |     | text |
| direction  | N   |     |     |     |     | C   |     |     |      |
| ---        |     |     |     |     |     |     |     |     |      |
| temp.      | Q   |     | L   |     |     |     |     |     | text |
| date       | Q   |     |     |     |     |     |     |     | text |
| longitude  | Q   | L   |     |     |     |     |     |     |      |

*table for 2024 exam*

| Variable  | D   | X   | Y   | Z   | T   | R   | —   | \[] | CP  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Country   | N   |     |     |     |     |     |     |     | tx  |
| Year      | Q   | P   |     |     |     |     | L   |     |     |
| Rank      | O   |     | P   |     |     |     |     |     |     |
| 2021 Rank | O   |     |     |     |     | C   |     |     |     |

- F column
	- we can transform the quantitative data to ordered by grouping the values
	- \> is used to denote no transformation
- we don't need to have the F, D' columns in the table
- multi-dimensional data
	- if we have more than 3 quantitative attributes, we need to use special approaches
		- only x, y, and size can properly capture Q
	- idea: reuse axes
	- solutions
		- scatter plot matrix
			- waste of space
				- symmetrical
				- the diagonal would contain diagonal – it is better to use a different graph (like a histogram)
			- difficult to see items
		- parallel coordinates
			- we use vertical axes to represent data
			- the horizontal axis is only used for visual separation
			- correlation
				- positive correlation – few crossing lines (mostly parallel)
				- negative correlation – most of the lines are crossing (in the middle)
			- to write it in the table, we would write Y→L for every variable
		- time series
			- horizon graph
				- $t\to X$
				- $\mathop{\mathrm{sign}} q\to$ color
				- $|q|\mathop{\mathrm{div}}H\to$ value (of the color)
				- $|q|\mathop{\mathrm{mod}}H\to Y$
				- $H$ … height of the slice we use
				- = composite visual mapping
					- we split one data attribute into multiple graphic variables
- composite visual mapping
	- (at least) one data attribute is mapped onto (at least) two graphic variables
- project
	- during the holidays: https://mosig.imag.fr/ClassNotes/UIS-IV-D3
		- after the holidays, we will get the dataset
			- questions … what questions do we want to answer using the dataset?
	- D3.js helps us manipulate the basic elements of the webpage
	- goal of task 0 (Anscombe) – instead of the tables, we want charts
		- see http://iihm.imag.fr/blanch/teaching/infovis/tps/0-anscombe/
		- references here: http://iihm.imag.fr/blanch/teaching/infovis/tps/
	- task 1 – penguins, Simpson's paradox
	- we have to submit the two tasks before the next lecture (3 nov)
- interaction
	- ScatterDice – choosing axes for the graph
	- Zoomable Treemaps
		- treemap of the internet
		- large collections are divided by initial numbers
		- clicking zooms by one level
		- but I can also draw a stroke → it zooms to the smallest node which contains the whole stroke
		- sometimes, the animation is controlled by the interaction
	- NodeTrix – hybrid visualization of graphs
		- how to express graphs traditionally
			- diagram – chaotic for large graphs
			- adjacency matrix – difficult to find longer paths
		- NodeTrix combines both approaches
		- social network
			- few nodes with a lot of connections (a lot of nodes with few connections)
			- adjacency matrix is useful to see if some nodes form a clique
	- similarity
		- we need a measure of similarity for two items and for two groups
		- dendrogram – tree representing the similarity of items
			- the lower is the common ancestor of the items, the more similar they are
			- we can cut the dendrogram at some level to get clustering
		- we can use dots in matrix to visualize similarity (the larger the dot, the more similar the items are)
			-  we can reorder the items to minimize differences between neighbors
			- that way, we get clusters
			- the matrix is symmetrical so we only need one half → dendrogramix
		- we can see relations that would disappear in the dendrogram
		- the app supports dragging items
			- if the feedback is continuous, we can track the changes
- when interacting directly with the visualization (not through “external” controls), we need to project from the screen space to the data space
- project
	- individual (but we can discuss), report sent to the teacher
	- chess ratings
	- if you don't play for a year, you're considered inactive and should not be listed among top-k players
	- in the monthly data, they may be missing rankings of players who did not play during the month
	- months are not converted to Date object as the conversion takes too much time
		- we can use lexicographical order
	- there will be a smaller dataset for testing purposes
	- we can do custom preprocessing in a different language
	- ranking of a federation – average over its top 10 players
	- there will be some changes in the repository during this week
	- questions
		- categories: getting global insights, focusing on subsets, comparing subsets, *focusing on specific items* (will be added)
	- visual design
		- visual mapping
		- explain why this mapping
		- description of interaction
		- sketch (pen and paper works well)
	- sending
		- it is preferred if we include the scripts used for preprocessing and instructions how to preprocess the data
		- we should not send the dataset as it's large
	- in the design phase, we can envision fancy stuff even if we cannot implement it afterwards

# Graphs

 - graph = vertices, edges (can be directed)
 - network = graph with attributes on the vertices and/or the edges
 - graph theory provides metrics
	 - vertices – degree, centrality
	 - (sub)graphs – diameter, density, connected components
	 - we can also compute metrics from the attributes (cost of a path if we have valued edges)
- tasks
	- vertices – finding neighbors, degree
	- paths – finding shortest paths, cycles
	- graph – finding cliques
- project
	- there's a simple python script for processing data
	- there are some smaller datasets available now
- visualization of graphs
	- we can even represent vertices as lines and edges as dots
	- hierarchical representation – no explicit edges, only hierarchy using enclosure
	- usual: node-link diagram
		- challenge – how to layout the nodes (“graph drawing”)
		- goal: optimize a quality metric (e.g. the number of links crossing)
		- for planar graphs – there can be no links crossing
		- sometimes, using attributes to compute the layout may be a good idea
- node-link layouts
	- linear layouts
		- even on a line, choosing the right order of the nodes is an interesting question
	- radial layouts
		- nodes on concentric circles
		- may be based on the selected node
			- it's better if the animation uses linear interpolation of polar coordinates
	- force-directed layout
		- attractive forces (links) and repulsive forces (nodes)
		- repulsion of nodes decreases with distance … $\frac1{d^2}$
		- attraction of two nodes connected by a link increases with distance … $d$
		- we need to compute the forces for all pairs of nodes
			- to get the final force of the node, we combine all the partial forces
		- problem: the initial random layout influences the final layout, there's no determinism
		- we can add constraints and generate a layout, which uses them
			- e.g. several nodes have to be on a line
			- Cola.js library
- node-link edges
	- edge-bundling
		- attractive/repulsive forces between segments of links → some links are bundled
		- very time consuming (quadratic number of edges, quadratic number of segment pairs)
		- another approach: computation in the pixel space
	- edge compression
		- power graph compression
		- there has to be a stopping condition for edge reduction
- adjacency matrix
	- vertices as rows and columns, edges as intersections
	- symmetrical for undirected graphs
	- we can represent all edges without overlapping or occlusion
	- hard to encode attributes of vertices – we can use the width of the line
	- patterns
		- central nodes – a lot of connections in one row/column
		- cliques – “squares”
			- if the rows/columns are in the correct order
			- → 1D layout problem, minimization of distances between vectors
			- we can use clustering
		- off-diagonal block pattern – kind of bipartite (sub)graph
		- bands pattern – “rings”
		- noise anti-pattern
			- hard to distinguish from badly ordered rows
		- bandwidth anti-pattern
			- if we sort the nodes in some special way (by their degree?)
			- it looks interesting but there's not interesting structure in the graph
	- Reorderable matrices (Bertin)
		- undirected bipartite graph → rectangular adjacency matrix
		- some reordering can be automatic, some can be manual
	- TableLens – spreadsheet with graphical visualization of attributes
	- for large graphs, node-link outperforms adjacency matrices only on tasks involving finding path
- trees
	- definition – DAG?
	- every vertex points to its parent (and stores other attributes)
	- tasks
		- find parent/children/siblings of a node
		- size/width/depth of a subtree
		- path to a node
	- layouts – node-link or nested
	- node-link
		- first approach
			- vertical coordinate corresponds to depth
			- to get horizontal coordinates, we start from the leaves and assign each leaf its coordinate (for parents, we can average their children or the leaves)
		- second approach
			- the same as first but in polar coordinates
		- collapsible subtrees
			- collapsed subtrees are represented by triangles (which corresponding width, height, and color)
			- SpaceTree
		- to get enough space, we may use hyperbolic geometry → we get infinite space (but infinitely small nodes at the edge of the circle)
		- it's probably a bad idea to use 3D for trees
	- nested layouts
		- TreeMap
		- nodes are rectangles, parents enclose their children (their subtrees)
		- if leaves have attributes (values) we can sum to get values for their parents, these attributes can correspond to the area (e.g. sizes of files)
			- simple implementation: we switch between splitting horizontally and vertically (slice and dice)
				- we still need to define traversal order
				- we have no control over aspect ratio
					- it's hard to compare areas of rectangles with too different aspect ratio
		- edges correspond to the enclosure
		- how to make the hierarchy understandable?
			- we can use colors and text orientation
		- nested circles waste a lot of space but look nicer
	- mixed layouts
		- Elastic Hierarchies
- one last lecture: exam preparation, we can go through the questions on the exam (we can see what we don't understand – then go through it together)