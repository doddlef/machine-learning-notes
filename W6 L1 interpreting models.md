## Interpreting models
tow primary ways:
- why a given model has miscalssified: **error analysis**
- why a given model has classified and instance in the way it has: **model interpretability**
### Error analysis
analysis of the sorts of errors:
- **identifying** different classes of error made
- **hypothesising** as to what has caused the different errors, and testing against the actual data
- **quantifying** whether it is a question of a data quantity / sparsity, or something more fundamental
- **feeding** those hypothese back into model

starting point: a confusion matrix & a random subsample of misclassified
a good starting assumption is that a given "cell" in the confusion matrix forms a single error class
- most error is actual class A be misclassified to B

tips:
- it is possible that different thins going on in a given cell, and multiple cells can also form a single class of errors
- always be sure to test hypotheses
- where possible, use the model assumption to guide the error analysis

### model interpretability
**hyperparameters**: parameters which **define and constrain the learning process**
**parameters**: what are **learned** when a given learner with a given set of hyperparameters is applied to a particulat trainint datset, and used to classify
- a model trained wiht a given set of hyper- can be interpreted relative to the parameters associated with a given test instance

#### KNN classifiers
- hyper-
	- neighbourhood size K
	- distance / similarity metric
	- weighting strategy
- parameters
	- none, as it is "lazy", so doesn't abstract aways from training instances
- interpretation
	- relative to the training instances that give rise to a given classification, and their distribution in the feature space

#### Nearest prototype classifiers
- hyper-
	- distance / similarity metric
	- feature weighting
- parameters
	- prototype for each class
	- size: $O(|C||F|)$
		- C = set of classes, F = set of features
- interpertations
	- relative to the distribution of the prototypes in the space, and distance to each prototype

#### Naive Bayes
- hyper-
	- smoothing method
	- optionally the choice of distribution used to model
- parameters
	- class priors and conditional probability for each feature class combination
	- size: $O(|C|+|C||FV|)$
		- C = set of classes, FV = set of feature-value pairs
- interpretation
	- usually based on the most positively-weighted features associated with a given instance

#### Decision Trees
- hyper-
	- attribute selection: information gain, gain ratio
	- stopping criterion
- parameters
	- decision tree itself
	- size: $O(|FV)$
		- FV = set of feature-value pairs
- interpretation
	- based on the path through the decision tree

#### SVM
- hyper
	- penalty term C for soft-margin
	- choice of kernel and and hyper- associated with it
	- how to deal with multi-class
- parameters
	- hyperplane: normal vector + intercept/bias
	- size: $O(|C||F|)$
		- C = set of classes, F = set of features for one-vs-all
- interpretations:
	- the absolute value of the weight associated with each non-zero feature in a given instance provides an indication of its relative importance in classifiaction

##### \_Chat-GPT: Hyperparameter and Hyperparameter Tuning
**Hyperparameter tuning** is the process of **finding the best settings** (hyperparameters) for a machine learning model to get the best performance.

It’s like tweaking the knobs of your model — not the parameters learned from data, but the **settings that control the learning process itself**.

**What Are Hyperparameters?**
These are values you set **before training** — they’re **not learned** by the model.
- **Parameters** are learned (like weights in a neural net).
- **Hyperparameters** are set manually or by search — they control how learning happens.

## Visualising Data

### Dimensionality Reduction
what if there are more than 3 attributes
- reduce down to 2 or 3 dimensions

### Principal component analysis
the principal components:
- are linear combinations of the original features
- are orthogonal to each other
- capture the maximum amount of variation in the data
generally performed using an eigenvalue solver

## Error analysis
evaluating the model, beyond just accuracy:
- what items are correctly / incorrectly classified
- what are most / least confidently classified
- how deos performance vary across classes

### Confidence
internal score for how well an items fits a class
- not the probability of the model being correct, though it may be correlated
- for different models
	- SVM: distance from classification boundary
	- Naive bayes:  posterior probabilities
	- K-NN




