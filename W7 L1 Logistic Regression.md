- is a classification model
- in linear regression, we have _continuous_ features and a _continuous_ output variable
- in classification, we have _continuous / discrete_ features and _discrete_ output variable

### regression to classification
- map continuous values onto discrete labels, by setting range of continuous variable that corresponds to each discrete class
- predict age group 11 - 20, ... instead of the value of age

### classification to regression
- **binary-class**: take class labels 0 and 1 as numeric values
- **multi-class**: build a set of regression tasks
- **approximate a _numeric membership_ for each class**

## Naive Bayes
![[navis-bayes_1.png]]
- strategy: attempt to model $P(c|x)$ directly
- assuming a 2-class problem
	- $P(c=Y|x)$:probability of an instance with class _Y_
		- if is _Y_: $P(c = Y|x) = 1$
	- if the numerical attributes of the instance are predictors, $P(c=Y|x)$ is the target variable:
		- $P(c=Y|x) = \beta * x = \beta_1 + \beta_1 x_1 + ... + \beta_D x_D$
![[probability-classification.png]] 

### Derivation
$P(c|x) = e^{\beta \cdot x}$
$\text{gaussian distribution} = \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$
- if $P(c|x) = e^{\beta x}$, then $\log P(c|x) = \beta \cdot x$
- Curve is unbalanced
	- fine granularity of response as $P \to 0$
	- coarse response as $P \to 1$
	- $P \gt 1$ when $\beta \cdot x \gt 0$![[exp.png]]

want same response behaviour for high and low _P_
using _logit_:
- $\text{logit} (P) = \log \frac{P}{1-P}$
- $\text{logit} (1-P) = \log \frac{1-P}{P} = -\text{logit} (P)$ ![[logit.png]]

### Logistic Regression
use linear regression to model $\text{logit P}$
- $\text{logit} P(c|x) = \log \frac{P(c|x)}{1-P(c|x)} = \beta \cdot x$
- $P(c|x) = \frac{1}{1+e^{-\beta \cdot x}}$, logistic function

### Training and Prediction
- training set: _N_ examples $(x_1, y_1), (x_2, y_2), ...,(x_N, y_N)$
	- $x_i = [x_{i0}, x_{i1}, ..., x_{iD}]$
- find the optimal $\beta = [\beta_0, \beta_1, ..., \beta_D]$
- predict a continuous valued output:
	- $P(c|x_{test}) = \frac{1}{1+e^{-\beta \cdot x_{test}}}$
- ![[predict_classification.png]]

## Decision Boundary
decision boundary still comes from $\beta \cdot x$
- given $\beta = [-3, 1, 1]$, $x = [1, x_1, x_2]$
- $c = Y \text{ when} -3+x_1 + x_2 \ge 0$

how do we determine $\beta$ ?
- define an objective function to optimise maximise accuracy / likelihood or equivalently minimise error
	- $\hat{\beta} = \text{arg max Likelihood} (\beta; L, F(T))$
	- gradient ascent or descent![[ascent_descent.png]]

assume a 2-class problem
- $\hat{P} (y = 1|x)$ is close to 1, when instance x has class label 1
- the likelihood:
	- $P(y = 1|x, \beta) = h_{\beta} (x) = \frac{1}{1+e^{-\beta \cdot x}}$
	- $P(y=0|x,\beta) = 1 - h_{\beta}(x)$
	- $P(y| x, \beta) = (h_{\beta}(x))^y (1-h_{\beta}(x))^{1-y}$
		- $y = 1$ => $h_{\beta}(x)$
		- $y = 0$ => ...
![[decision_boundary_exstiamte.png]]
![[decision_boundar_estimate_2.png]]

## Multi-class classification
multinomial logistic regression
- take one class as **pivot**
- for every other class $c_j$, build a regression model
	- treat class $c_j$ as class Y, and the pivot class as class N
- end up with |C| - 1 different logistic regression models
- predict the class label according to the one with the highest probability score
![[multi-class-classifiction.png]]
![[multi-class-derive.png]]

### \_Chat-GPT: multi-class classification
**1. Pick a Pivot Class**
Choose **one class** (say, $c_1$) as the **pivot** — a reference class. You will **not** train a model for this one.

**2. Train a Model for Every Other Class**
For every other class $c_j$ (where $j \ne 1$):
- Train a **binary logistic regression model** to distinguish between:
- Class $c_j$ = **Yes**
- Pivot class c_1 = **No**
So, for a total of k classes, you train k - 1 models.
Each model outputs the probability that x belongs to class $c_j$ **vs. the pivot**.

**3. Make Predictions**
For a new input x:
- Use each of the $k - 1$ models to get probabilities:
-  $P(c_j \mid x)$ vs. pivot
-  The probability for the **pivot** class is:
	$P(c_{\text{pivot}} \mid x) = 1 - \sum_{j \ne \text{pivot}} P(c_j \mid x)$, assuming probabilities are normalized.
- Finally, **predict the class with the highest probability**.
## summary
![[logist-regression-discuss.png]]

logistic regression
- forms a linear decision boundary
- provides probabilities of the classification result
- easy to interpret

## \_Chat-GPT: Logistic Regression
> Logistic Regression is a **classification algorithm** used to predict **binary outcomes** (like yes/no, 0/1, spam/not spam).

It does this using a **sigmoid function** to “squash” a linear combination of inputs into the range **(0, 1)** — i.e., a probability!

