## Feature vectors
a feature or attribute is any distinct aspect, quality or characteristic of an instance
- an n-dimensional vector

### similarity and dissimilarity
- similarity
	- numerical measure of how alike
	- higher when more alike
	- often \[0, 1]
	- nominal
		- 1 if p = q else 0
	- ordinal
		- 1 - $\frac{|p-q|}{n-1|}$
	- s = -1, s = $\frac{1}{1+d}$, or s = $1-\frac{d - min_d}{max_d-min_x}$
- dissimilarity
	- can be infinity, there are always something more dis-alike than one item

### Distance measure
- no negative
- zero from a point to itself
- symmetric
- triangle inequality

- given a dissimilarity measure, that d(A, B) = items in A but not in B
	- this is not a properly distance measure, against symmetric

#### Euclidean Distance
#### Manhattan Distance
#### Cosine Similarity

### Nominal variables ?
- convert category names to numbers
	- creates an artificial order when no order exist
- one-hot encoding
	- attribute with m possible values to m boolean attributes

## Nearest Neighbour classification
for any new instances, find the most similar instances use them to classification

### Data scaling / normalization
attributes may have different ranges, ensures all have similar ranges

man two common choices
- min-max to \[0-1]
- standardise to mean = 0 and std = 1

### choosing K
- smaller K lead to lower performance due to noise (overfitting)
- larger K tend to drive the classifier performance toward Zero-R performance

### weighted K-NN
according to the weighted accumulative class of the K nearest
- equal wight: always choose majority classes
- inverse linear distance: $w_j=\frac{d_max-d_j}{d_max-d_min}$
- inverse distance: $w_j=\frac{1}{d_j+c}$, c is a very small distance, avoid exactly same

### Break ties
- generally set K to odd
- random pick
- find another instances
- take class with highest prior probability

### Implementation
- K-NN is lazy, the time we save in training is lost if we have to make many predictions
- classical machine learning models (Bayes, decision trees) are generally much smaller than the dataset
	- some modern models (GPT) are about the same

### Strengths
- simple, instance-based, model free
- flexible decision boundaries
- incremental (can add extra data)
### Weakness
- requires a useful distance function
- arbitrary K value
- lazy learner
- prone to noise and high dimenions