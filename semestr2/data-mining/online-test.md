# Online Test

## Introduction

- data mining from databases
	- non-trivial process of gaining implicit, previously not known, but potentially useful information from the data
	- originated in the 90s (there was not enough data before)
	- knowledge discovery in databases (KDD)
	- data mining (DM) – business intelligence (BI) and big data
- foundations
	- artificial intelligence, machine learning methods
	- database systems (to store large data sets), information retrieval
	- statistics – modeling and analysis of dependencies found in the data
	- \+ how to use the results for decision-making
- data mining is an interactive and iterative process
	- data preparation – we build one table containing all the relevant data
		- selection, preprocessing, transformation
	- the actual “data mining” – we find *patterns* in the data
	- interpretation – found knowledge shall be evaluated from the point of view of the end user (manager, customer, etc.)
- PoV of a manager
	- there's a topical issue
	- goal of the data mining process is to obtain as much information as possible that is relevant to solving the problem
	- example
		- find groups of customers of a department store to offer special services to
		- the found groups can be interpreted as segments in the given market area
	- steps
		- form a team: data analyst, domain expert, expert on databases, …
		- specify the problem
		- obtain all data available
			- we should also obtain the external data describing the environment of the analyzed processes (time period of the year, advertising, political issues, weather, …)
		- select the methods
			- clustering, classification, exploratory data analysis, association rules, decision trees, genetic algorithms, Bayesian networks, neural networks
			- visualization methods – helpful for presentation
		- preprocess the data
		- mine the data
		- interpret the results
			- we may need to create an analytical report
			- make the results easy to understand
			- the output can also mean to carry out a reasonable action
- tasks
	- classification and prediction
		- goal: predict a continuous or discrete value based on some attributes
		- interpretation may be challenging
		- prediction: weather forecast, stock prices, …
		- we should be able to cover the entire domain (all the data may be useful for a reasonable prediction)
	- description
		- goal: find a dominant structure or relationships
		- we may ignore some of the information; the extracted knowledge does not need to be that precise (but it should be easily understandable)
	- looking for “nuggets”
		- goal: find some interesting knowledge (does not have to fully cover the given concept)
- real tasks (examples)
	- segmentation and classification of bank clients
	- causes of failures in telecommunication networks
	- causes of change of service provider
	- prediction of power consumption
	- analysis of the patient database in a hospital
		- Florence Nightingale
		- Ignaz Semmelweis
	- market basket analysis

## Methodologies

- goal: provide the users with a unified framework; guide data mining applications regardless of industry
	- it's necessary to have high-quality data
	- the steps are usually iterative
- SEMMA
	- sample – select data for modeling
		- may include sampling, imputation (adding other useful information, e.g. adding seasons of the year to the data about the sales), partitioning (train-test-validation split)
	- explore – visual exploration and dimensionality reduction
	- modify – prepare the objects, values, and variables for data modeling; transform the data
	- model – apply data mining techniques (decision trees, regression models, NNs, …)
		- create models providing relevant outcome
	- assess – evaluate the results of modeling (assess their reliability and usefulness)
- CRISP-DM
	- cross-industry standard process for data mining; a robust general-purpose model
	- 6 phases (their order is not strict)
		- business understanding
			- determine our business objective
			- assess our present situation, what resources and data we have
			- risk assessment
			- setting KPIs
		- data understanding
			- collect and describe initial data; explore and visualize it
			- verify the quality of the data
		- data preparation
			- cleaning, integration (merging), aggregation, …
			- make the dataset ready for further analysis and modeling
		- modeling
			- select the modeling technique
			- generate test design
			- build the model
			- assess the model
		- evaluation
			- evaluate the results – from the point of view of the manager
			- review the process
			- determine the next steps
		- deployment
			- results should be presented in a simple and comprehensible way
			- plan the deployment (what steps should be done)
			- final report, review the project
				- to preserve knowledge
	- ciritique
		- little support for project management
		- what to do if there are problems?
		- → IBM released Analytics Solutions Unified Method for Data Mining (ASUM)
- ASUM
	- phases
		1. analyze – define the needs (desired features, performance, usability, …), obtain agreement
		2. design – define solution components, identify resources, clarify requirements
		3. configure & build – including testing and validation
		4. deploy – create a plan to run and maintain the solution
		5. operate & optimize – preserve the health
		- \+ project management – there are processes that help to monitor the progress and maintain the project
	- benefits
		- minimized risk
		- scalable and enterprise-ready
		- comprehensive
		- product-specific implementation roadmaps

## Data Analysis

- types of attributes
	- interval-scaled attributes – their values are real number following a linear scale
	- ratio-scaled attributes – follow an exponential scale → need to be log-transformed ($\log x_i$) before treating them like interval-scaled attributes
	- a nominal attribute can be transformed to a series of binary attributes (one-hot encoding)
	- ordinal attributes are sometimes treated as interval-scaled attributes
- data standardization of interval-scaled attributes
	- decimal scaling – divide the data by the smallest power of 10 to get them to the interval $[-1,1]$ (while maintaining the mutual relations)
	- range standardization
		- to $[0,1]$ … $\frac{x-\mathrm{min}}{\mathrm{max}-\mathrm{min}}$
		- to $[-1,1]$ … $2\cdot \frac{x-\mathrm{min}}{\mathrm{max}-\mathrm{min}}-1$
	- Z-score standardization … $\frac{x-\mu}{\sigma}$
		- $\mu$ … mean
		- $\sigma$ … corrected sample standard deviation
			- $\sigma=\sqrt{\frac1{n-1}\sum_{i=1}^n(x_i-\mu)^2}$
		- or we can use the *corrected* sample standard deviation
	- standardization according to the mean absolute difference
		- $\frac{x-\mu}{s}$
		- where $s=\frac1n\sum_{i=1}^n|x_i-\mu|$
- range, quartiles, outliers
	- range = difference between the highest and the lowest value in the set
	- quartiles – values $Q_1,Q_2,Q_3$
		- 25% of the observations below $Q_1$ (lower quartile)
		- 50% below $Q_2$ (median)
		- 75% below $Q_3$ (upper quartile)
	- interquartile range $IQR=Q_3-Q_1$
	- formulas (for discrete data)
		- $Q_1=x_{\lceil n/4 \rceil}$
		- $Q_3=x_{\lceil 3n/4 \rceil}$
		- but if $x_{n/4}$ or $x_{3n/4}$ exists ($n$ is divisible by 4), we need to average this value with the next one $($$x_{n/4+1}$ or $x_{3n/4+1}$)
	- outlier is any value $\notin[Q_1-1.5\cdot IQR,\ Q_3+1.5\cdot IQR]$
	- box plot
		- box … between $Q_1$ and $Q_3$ with a mark (line) representing the median
		- two other lines … boundaries for outliers (or the extrema that are not outliers)
		- other marks outside … individual outliers

---

### Regression Analysis

- motivation
	- it may be costly to obtain output values
	- input values are known earlier than the output (we want to estimate the output)
	- controlling input variables may lead to the desired behavior of the output
	- we want to find a (causal) relationship between the input and the output
- correlation analysis – is there a linear relationship between two numerical quantities?
- linear regression – what are the parameters of the linear relationship between two numerical quantities?
- least squares method
	- find parameters $\alpha,\beta$
	- set partial derivatives equal to zero
		- $n\alpha+\beta\sum_i x_i=\sum_i y_i$
			- or $\alpha=\bar y-\beta\bar x$
		- $\alpha\sum_i x_i+\beta\sum_i x_i^2=\sum_i x_iy_i$
	- so $(\bar y-\beta\bar x)\sum_i x_i+\beta\sum_i x_i^2=\sum x_iy_i$
	- we get $\beta=\frac{\sum_i (x_i-\bar x)(y_i-\bar y)}{\sum_i(x_i-\bar x)^2}$
- correlation coefficients
- multi-dimensional regression
	- linear → least-squares method in matrix form
	- non-linear
		- logistic regression
- discriminant analysis
	- classification into classes

### Cluster analysis

- we want to divide the observed patterns into groups of mutually similar patterns
	- assumption: we can measure the distance between patterns
- Minkovski metrics
	- Hamming distance … $L_1$
	- Euclidean distance … $L_2$
	- Chebyshev distance … $L_\infty$
- Mahalanobis distance
	- uses the covariance matrix
- distance between two clusters
	- method of the nearest neighbor
	- method of the farthest neighbor
	- method of average distance
	- centroid method
- centroid
	- compute the average over all the features
	- but such pattern may not be in the data at all
- k-means clustering
	- several variants
- k-medians – just use Hamming distance instead of Euclidean
- hierarchical clustering
	- dendrogram
- learning vector quantization (LVQ)
	- no guarantee of convergence (?)
- k-medoids
	- uses a similarity measure instead of averaging
	- we consider $k$ best representatives (from the dataset)
		- so the medoids are real data points
- grid-based methods (e.g. MAFIA)
	- which cells of the grid are densely covered by the data?
	- merge neighboring *dense* hyper-cubes (cells) to get clusters
- density-based algorithms
	- core point: there at least $\tau$ points closer than $\varepsilon$
	- border point: there is at least one core point closer than $\varepsilon$
	- noise point: otherwise
- scalable approaches – for lots of data
	- CLARA, CLARANS
	- k-medoids are expensive to compute
	- CURE

## Decision Trees

- difficult to process continuous data
	- decision trees divide the features space into rectangular regions
	- problem if the decision boundary looks like $y=x$
		-  we would need to check a value of one attribute relatively to another attribute
- several algorithms
- pruning
- bagging
	- reduces the variance
- random forests
	- deal with problems of pairwise correlation of models constructed using bagging
- boosting
	- reduces the bias