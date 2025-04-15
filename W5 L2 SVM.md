## Nearest Prototype Classification
- a parametric variant of nearest-neighbour classification
- calculate the _centroid_ of each class, and classify each test instance according to the class of the centroid it is nearest to
for a class $C_j$ with _M_ instances ${x_i: [a_{i,1}, ..., a_{i,D}]}$
- prototype $P_j$ = $[a_1, a_2, ..., a_D]$ 
- each $a_d = \frac{\sum_{i=1}^{M} a_{i,d}}{M}$

### \_Chat-GPT: Nearest Prototype Classification:
Nearest Prototype Classification assigns each class one or more **representative points** called **prototypes**. When a new input comes in, it is classified based on its **distance to the nearest prototype**.

You can think of it like:

👉 _“Each class has one or a few representatives. Which one are you closest to?”_

**💡 How It Works:**

1. **Training Phase (Eager Learning):**

• Instead of storing all training data (like KNN), the algorithm learns one or more **prototypes** per class.

• These prototypes are usually **centroids** (averages) or optimized locations in the feature space.

2. **Prediction Phase:**

• For a new input, compute the **distance** (usually Euclidean) to each prototype.

• Assign the label of the **closest prototype**.

**📈 Pros:**

• Much **faster** than KNN at prediction time.

• More **compact** — doesn’t store all training data.

• Easy to implement and interpret.

**🧪 Variants:**

• **Learning Vector Quantization (LVQ):** Learns multiple prototypes per class and adjusts them using gradient-based rules.

• **Prototypical Networks:** Used in few-shot learning — learns prototypes in a learned embedding space.


## SVM (support vector Machine)
find a straight / hyperplane separates two classes
- linear separability
 ![[linear_sparaility.png]]
 ![[linear_classifier.png]]
$2x_1 + x_2 - 4 = 0$ <=> $[2\space1][x_1\space x_2]^{T} - 4 = 0$

- many solutions => many lines can divide the tow classes, but we want it to in the middle, not too close with each class
- the closer to the line, the less confident in the prediction

### optimal solution
find a decision boundary that allows to make all correct and confident (far from the decision boundary)
- SVM finds an optimal solution
	- maximises the distance between the hyperplane and the difficult points close to decision boundary
	- most stable under perturbations of the inputs

width of margin
![[width_margin.png]]

### Classification using SVM
 ![[SVM.png]]
 how to learn $w$ and $b$, we need find
 - correctly classifies all points
 - widest margin possible
is a convex problem, can be solved using quadratic programming
![[SVN_2.png]]
**not a lazy model**
#### \_Chat-GTP: Not a lazy model
**🐢 KNN - Lazy Learning**

• **Lazy model**: It **doesn’t do much during training**.

• Just stores the training data.

• **All the work is done during prediction**: it finds the closest neighbors and decides based on them.

• This makes **training fast** but **prediction slow**, especially for large datasets.

  

**⚡ SVM - Eager Learning**

• **Eager model**: It **learns a decision boundary** (a hyperplane) **during training**.

• It optimizes to find the best separating hyperplane with the **maximum margin**.

• So, training is more complex and computationally intensive.

• **Prediction is fast**, since it’s just evaluating which side of the boundary a point lies on.

### Non-linear SVM
make non-linearly separable problem separable
- map data into better representation space
- $R^2 => R^3$

### Multi-class SVM
convert to two-class problem:
- one-versus-all: one classifier to seperate one class from the rest of classes, choose the class which classifies test data point with greatest margin
- one-versus-one: one classifier per pair of classes, choose the class selected by most classifiers
Training time can be a serious issue, need to build many SVMs 
![[one_vs_all.png]]

### Summary
- a linear hyperlane-based classifier for a two-class
- select the hyperplane with maximum margin
- _soft margins_ allow some data points to violate the separating hyperplane
