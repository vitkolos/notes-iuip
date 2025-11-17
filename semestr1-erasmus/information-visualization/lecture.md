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