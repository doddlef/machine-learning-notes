for classification problems, classes are categorical
- attribute can be categorical or continuous
- what if the concept (output) were continuous

## Regression
continuous attributes -> continuous concept
assuming a linear relationship between attribute values $a_k$ and the continuous concept $c$: we have
	$c = w_0 + \sum_{k=1}^{D} w_k a_k$
	where $w_k$ is a weight corresponding to $a_k$

### Linear regression
captures a linear relationship between:
- an outcome variable y
- one or more predictor $x_i$

capture changes in one variable that correlate linearly with changes: $y = \beta * x$

find the optimal $\beta = [\beta_0, \beta_1, ...]$

### fitting
choose the best line: minimise the distance between al points and the line
![[linear_fit_model.png]]
## Parameter estimation
### Optimisation
given an evaluation metric M (like accuracy or error), a dataset T (consiting of attributes X and labels y) and a learner L with parameters $\theta$
- maximise or minimise $M(\theta; L, T)$, where learner L and dataset T are fixed
- if M is error rate
	- $\theta = arg \space min_{\theta \in \Theta} Error (\theta; L, T)$
finding parameters that optimise some criterion M for model L and dataset T

### hot to find optimal solution
- analytic solution
- exhaustive solution
	- grid search
- iterative approximation

#### Analytic solution
- closed form, can be computed exactly
- requires solving a system of equations:
	- $\frac{\delta (Error)}{\delta \theta_1} = 0, \frac{\delta (Error)}{\delta \theta_2} = 0, \frac{\delta (Error)}{\delta \theta_3} = 0, ...$
- for linear regression: $\theta = (X^T X)^{-1} X^T y$
- challenges: derivatives can be undefined or not calculable

linear regression:
![[linear_analytic.png]]
![[linear_analytic_2.png]]
##### \_Chat-GPT: analytic solution:
A solution that can be **calculated directly** using formulas — no trial and error, no guessing.

**✅ Features:**
• Involves **closed-form equations** (e.g., solving a system of equations).
• **Fast and exact** (assuming perfect conditions).
• Usually only possible for **simple or convex problems**.

**📘 Example:**
• Linear regression without regularization:
$\theta = (X^TX)^{-1}X^Ty$
This gives you the optimal weights directly.

#### Exhaustive solution
![[exhaustive_solution.png]]
- what about parameters that are continuous:
- using **grid search**
- for each numerical $\theta \in R$
	- identify boundaries of range $R_{-}, R_{+}$
	- divide range $[R_{-}, R_{+}]$ into equal-width samples
	- calculate Error for each sample

##### \_Chat-GPT: exhaustive solution:
Try **all possible combinations** and pick the best one. It’s brute-force.

**✅ Features:**
• Guarantees the **optimal solution** (if the search space is finite and fully explored).
• But can be **computationally expensive** or even infeasible for large spaces.

**🧰 Includes:**
**🔹 Grid Search:**
• A **systematic way** to try combinations over a grid of parameter values.
• Often used in hyperparameter tuning:
```python
for lr in [0.01, 0.1, 1.0]:
    for batch_size in [16, 32, 64]:
        train_and_validate(lr, batch_size)
```
• Easy to parallelize, but **inefficient** in high dimensions.

**📘 Example:**
• Tuning SVM hyperparameters (like C and gamma) using a grid of values and picking the one with the highest validation accuracy.

#### Iterative Approximation
![[iterative_solution.png]]

Gradient Descent:
- using a learning rate $\alpha$
![[gradient_DESCENT_1.png]]![[gradient_descent_2.png]]
![[gradient_descent_3.png]]
$\beta^{iter +1}_k$ stands for $\theta^{iter +1}_k$
![[gradient_descent_4.png]]

##### \_Chat-GPT: Iterative Approximation
Start with a guess, **improve it step by step**, and stop when it’s “good enough”.

**✅ Features:**
• Useful for **complex or high-dimensional problems** where analytic solutions don’t exist.
• Each step tries to **reduce the error** or **optimize the objective function**.

**🧰 Common methods:**
• **Gradient Descent**
• Newton’s Method
• EM Algorithm
• Stochastic methods (like SGD)

**📘 Example:**
• Training a neural network with backpropagation:
• Start with random weights.
• Use **gradient descent** to iteratively update weights:
$\theta \leftarrow \theta - \alpha \nabla J(\theta)$

## Linear Regression Evaluation & extension
doesn't make sense to evaluate numeric prediction tasks in the same manner as classification tasks
many scoring, all of which based on the absolute or relative difference between the predicted value and actual value

MSE, RMSE, RRSE:
![[evlaution_matrix.png]]
correlation coefficient (Pearson's correlation): statistical correlation between predicted and actual values:
![[persona.png]]
### extension:
linear regression is an intuitive model, with easy implementations:
other methods:
- regression trees
- locally weighted linear regression
- support vector regression
#### beyond linear relationship:
![[polynomial_linear.png]]
