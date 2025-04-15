## One R (one rule)
simple baseline for discrete data classification
- for each attribute
	- assign each level of that attribute to the most likely class
	- calculate error rate of this approach
- compare error rates of all attributes and select the attribute with the lowest classification error rate - this attribute is the "one rule"

### example
- if sunny, 0.4 = true, 0.6 = false => sunny = false
- if overcast, 1 = true, 0 = false => overcast = true
- if rainy, 0.6 = true, 0.4 = false => rainy = true

## constructing decision trees: ID3
construct decision trees in recursive divide-and-conquer fashion
- if all instance have same label, then stop
- else 
	1. select an attribute to use in partitioning Root node instances
	2. create a branch for each attribute value and partition up Root node instances according to each value
	3. Call ID3 for each for each leaf node

## pick attribute

### entropy
recall it is a measure of unpredictability
- if most of the probability mass is assigned to a single event
	- predictable -> low
- else 
	- high

in context of decision trees, want leaves with low entropy

#### information gain
the expected reduction in entropy caused by knowing the value of an attribute
- entropy before splitting the tree using attribute's values
- weighted average of the entropy over the children after the split
if the entropy decreases, better

### mean information
weighted average of the entropy over the children after split
$MeanInfo = \sum_{}^{} {P(x)H(x)}$

### Information Gain
select attribute best splits the instances at a given root node R according to information gain: $IG(R_{A}|R) = H(R) - \sum_{j = 1}^{m} P(x_{j}) H(x_{j})$

prefer highly-branching attributes
- may be overfitting ?
- suppose we have a label id, which contains only 1 items for each instances, it will be 0, which will be definitely chosen

### Gain Ratio
reduces the bias for information gain towards highly-branching attributes by normalising relative to the split info

- split info is the entropy of a given split
![[gain ratio.png]]

### ID3
- ID3 is an inductive learning algorithm
- search a space of hypotheses for one fits training examples
- performs a simple-to-complex, hill-climbing search
	- start with empty tree
	- no backtracking
- prefer the shortest hypotheses fit the training set
- fast

## Variants of decision trees
- random trees: use a sample of the possible attributes at a given node
- C4.5
