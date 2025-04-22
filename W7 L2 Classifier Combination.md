(or ensemble learning) constructs a set of **base classifiers** from training data and performs classification by **aggregation** the outputs made by each base classifier

![[classifier-combination.png]]

intuitions:
- take into account the opinions of several experts rather than relying only on one
- the combination of lots of weak classifiers can be at least as good as one strong classifier
- the combination of a selection of strong classifiers is (usually) at least as good as the best of the base classifiers

### Does combination work?

![[does_combination_work.png]]

when does the combination work?
- the base classifier do not make the same mistakes
- each base classifier is reasonably accurate

### construct base classifiers
- **instance manipulation**: generate multiple training datasets through sampling, and train a base classifier over each
	- bagging
- **feature manipulation**: generate multiple training datasets through different feature subsets, and train a base classifier over each
	- random forest
- **algorithm manipulation**: semi-randomly tweak internal parameters within a given algorithm to generate multiple base classifiers oven a given dataset

the simplest means of classification over multiple base classifiers is voting:
- for nominal classes, run multiple base classifiers over the test data and select the class predicted by the most base classifiers
	- KNN
- for continuous output, average over the numeric predictions of our base classifiers

### Bias and Variance
analysing the generalisation error of a predictive model
from model perspective:
- **Bias**: the tendency of a classifier to make systematically wrong predictions
	- 准
- **Variance**: the tendency of producing different models or predictions for different training sets using same learner
	- 精
lower bias and lower variance $\to$ better generalisation
![[bais_and_variance.png]]

## Bagging
bootstrap aggregating
- intuition: the more data, the better performance (lower the variance), so how can we get more data?
	- construct new datasets through a combination of **random sampling and replacement**

### sampling examples
- randomly sample the original dataset _N_ times, with replacement
- we get a new dataset of the same size, where any individual instance is absent with probability $(1-\frac{1}{N})^{N}$
- construct _k_ random datasets for _k_ base classifiers, and arrive at prediction via voting![[bagging.png]]

### Classification
- the same base classification algorithm is used throughout
- reduces the variance of predictions
- effective for unstable classifiers
	- unstable: small changes in the training set result in large changes in predictions, e.g. DTs
	- may slightly decay the performance of stable classifiers, e.g kNN

- simple method
- possibility to parallelise computation of individual base classifiers
- effective over noisy datasets, as the outliers may vanish
- performance is generally significantly better than the base classifiers and only occasionally substantially worse

## Random Tree
a decision tree, but only some of the possible attributes are considered at each node
- e.g., a fixed proportion $\tau$ of all attributes
- faster to build than a deterministic decision tree, but increase model variance
- decision tree![[decision-tree.png]]

an ensemble of Random Trees, many trees = forest
- each tree is built using a different Bagged training dataset
- the combined classification is via voting![[random-forest.png]]

- hyperparameters:
	- number of trees _B_, which can be tuned based on "out of bag" error
	- feature sub-sample size: as it increases, both the strength and the correlation increase: $\left\lfloor (\log_{2} |F| = 1) \right\rfloor$
- interpretation:
	- logic behind predictions on individual instances can be followed through the various trees

practical properties:
- generally a very strong performer, efficient to construct
- parallelisable
- robust to overfitting
- interpretability sacrificed

## Boosting
- intuition: tune base classifiers to focus on the hard-to-classify instances
- method: iteratively change. the distribution and weights of training instances to reflect the performance of the classifier on the previous iteration
	- start with sampling: each training instance have $\frac{1}{N}$ probability of being included in the sample
	- over _T_ iterations, train a classifier and **update the weight of each instance** according to whether it is correctly classified
	- combine the base classifiers via **weighted voting**

![[boosting_1.png]]
![[boosting_2.png]]

- initialize a weight vector with uniform weights
- loop
	- apply a weak leaner to weighted training examples
	- increase weight for misclassified examples
- majority voting on. trained classifier

### AdaBoost
![[ada_1.png]]
![[ada_2.png]]
![[ada_3.png]]
![[ada_4.png]]

## Comparison

| Bagging/Random Forest    | Boosting               |
| ------------------------ | ---------------------- |
| parallel sampling        | iterative sampling     |
| simple voting            | weighted voting        |
| homogeneous classifiers  | homogenous classifiers |
| minimise variance        | minimise instance bias |
| not prone to overfitting | prone to overfitting   |

## Stacking
- intuition: smooth errors over **a range of algorithms** with different biases
- method 1: voting? which classifier to trust?
- method 2: train a meta-classifier (level-1 model) over the outputs of the base classifiers (level-0)
	- learn which classifiers are reliable
	- train using nested cross validation to reduce bias

- **L-0**: base classifiers
	- given training dataset $(X, y)$
	- train different classifiers: e.g. SVM, Naive Bayes, DT, ...
- **L-1**: combination
	- construct new attributes based on Level-0 classifiers
		- each attribute contains the predictions of a L-0 classifier, if there are _M_ level-0 classifiers, add _M_ attributes
		- discard or keep original data _X_
		- consider other data if available (probability scores, weights of SVM)
	- train meta-classifier (logistic regression) to make final prediction

![[stack_1.png]]
![[stack_2.png]]![[stack_3.png]]

- able to combine heterogeneous classifiers with varying performance
- mathematically simple but computationally expensive method
- generally, stacking results in as good or better results than the best of the base classifiers