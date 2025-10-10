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
- example: gaminder
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

| Variable  | D     | F   | D'    | X   | Y   | Z   | T   | R   | —   | \[] | CP  |
| --------- | ----- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| Number    | Q     |     | Q     | L   | L   |     |     | S   |     |     |     |
| Direction | N     |     | N     |     |     |     |     | C   |     |     |     |
| Town      | N     |     | N     |     |     |     |     |     |     |     | tx  |
| Lon.      | QXlon |     | QXlon |     |     |     |     |     |     |     |     |
| Lat.      | QYlat |     | QYlat |     |     |     |     |     |     |     |     |
| Date      | Q     | f   | Q     |     |     |     |     |     |     |     | tx  |
| Temp.     | Q     | f   | Q     |     | P   |     |     |     | L   |     | tx  |

*table for 2024 exam*

| Variable  | D   | F   | D'  | X   | Y   | Z   | T   | R   | —   | \[] | CP  |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Country   | N   |     | N   |     |     |     |     |     |     |     | tx  |
| Year      | Q   |     | Q   | P   |     |     |     |     | L   |     |     |
| Rank      | O   |     | O   |     | P   |     |     |     |     |     |     |
| 2021 Rank | O   |     | O   |     |     |     |     | C   |     |     |     |
