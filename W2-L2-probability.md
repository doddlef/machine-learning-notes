# ML W2 L2 Probability

## variables
variable has various types
* nominal / categorical variable
    * discrete types or categories: sunny, overcast, rainy...
    * no natural ordering of the values, equally dissimilar from each other
    * boolean is a special type of nominal
* ordinal variable
    * has discrete values, but a natural order
    * small, medium, large
* continuous /numerical variable

## distribution
### Discrete uniform distribution
### Binomial distribution
### multinomial distribution
a series of independent trials with more than two outcomes
### Gaussian (normal) distribution

## Entropy
measure of information
* how much information is available for learning?
* how much did the model learn?
* are two models representing the same information?

- measure of unpredictability
- measured in bits
- the entropy of a discrete random variable X with, x1, x2, ... is: $- \sum_{i=1}^{n} P(x_i) \log_2 P(x_i)$
  - a fairy coin flip P(heads) = 0.5
    - H(X) = - 0.5 * $\log_2 0.5$ - 0.5 * $\log_2 0.5$ = 1
  - P(heads) = 0.9
    - H(X) = - 0.9 * $\log_2 0.9$ - 0.1 * $\log_2 0.1$ = 0.47
- it depends on both the number of possible state, and the likelihood of states
    - low = highly predictable
    - high = unpredictable
- range depends on number of possible outcomes
    - 2 outcomes: 0 - 1
    - N outcomes: 0 - log(n)
    - = 0 means only one outcome is possible
    - = log(n) means all outcomes equally likely

### example: text
if every letter is equally likely to appear, 26 letters = 26 outcomes = log(26) = 4.7 bits, and actual entropy = 4.14
> minimum letters needed to achieve this entropy = 2^4.14 = 17.63
