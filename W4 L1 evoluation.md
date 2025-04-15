
## Classifier
assign correct class labels
- train on some training data
- test on test data (not seen before)
- evaluate

- accuracy: number of corrected / total number = (TP + TN) / (TP + FP + TN + FN)

## Test set

### Random holdout
randomly partition data into "training" or "test"

### Repeated random subsampling
random holdout repeated multiple times, final evaluation is average over all iterations

### Cross validation
split into m partitions, iteratively select one partition as test, the others are training data.
- evaluation metric is aggregated across m partitions
- every item appears as a test item exactly once
- Leave-one-out cross-validation
	- m = N
	- maximises training data

### Practical issues
- should we ensure proportion of class in training v.s. test set
	- random sampling may produce different proportions
	- stratification or vertical sampling: training data adn test data both have the same class distribution

## Validation set
sometimes: split into train/validation/test
- a "test" set for training data
	- choose weights or parameters
	- check if model converged to a good solution

## Types of errors
- results
	- TP: true positive
	- FN: false negative
	- FP
	- TP
- Accuracy = ${\frac{TP + TN}{TP + FP + FN + TN}}$
- Error rate = $\frac{FP+FN}{TP+FP+FN+TN}$
- eddor rate reduction = $\frac{ER_{0} - ER}{ER_{0}}$
	- change in error rate relative to a base model's error rate

### Precision
how often is the model correct, when predicts a positive: $\frac{TP}{TP+FP}$

### Recall
what proportion of the true positive was able to detect: $\frac{TP}{TP+FN}$
- want to detective all positive case
	- positive Covid 19, and we always want find all patient

### F-score:
both precision and recall to be high: $\frac{2PR}{P+R}$

### sensitivity
another name for recall - the proportion of true positive cases the model was able to detect

### specificity
proportion of true negative cases that the model was able to detect (opposite of recall): $\frac{TN}{FP+TN}$

### Confusion matrix
each row represent actual classes, each column represent classified

## Multi-class evaluation
- macro-averaging: calculate Precision and Recall per class and take mean
- micro-averaging: combine all instances into one pool
	- all correct is true positive
- weighted averaging: calculate P, R per class, take mean and weighted by proportion of instances in that class

## Baseline and Benchmark
- baseline = simple method expect any machine learning method to bead
	- random guessing
- benchmark = established rival technique to which we are comparing out method

### common baselines
- random guessing
- zero-R baseline: guess the most common label in the training set
- regression: mean value
- object detection: middle of the image
