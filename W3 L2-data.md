Bayes assume nominal data, but not continues data, using bins  
  
## Nominal to Numeric  
### one-hot encoding:  
* attribute with m possible values -> m boolean  
  * bus = \[1, 0, 0]  
  * tram = \[0, 1, 0]  
  * car = \[0, 0, 1]  
* best way to represent nominal values in a continuous, but increases dimensionality  
  
### Discretion  
two steps  
* how many nominal values  
* where to place boundaries  
  
options  
* equal width  
* equal-frequency  
* clustering (k-mean)  
* supervised discretion  
  * group values into class-contiguous intervals  
  
## Gaussian  
usually gaussian distributing if fit for many statics  
* calculate the mean and SD to from data set  
* then using the pdf to get the probability  

![[gaussian_1.png]]![[guassian_2.png]]![[guassian_3.png]]
  
## Types of Bayes  
* Multivariate: attributes are nominal, and can take any of a fixed number of values  
* binomial: attributes are binary  
* multinomial: attributes are natural numbers corresponding to frequency  
  * P(A = 2, B = 1, C = 3, ...)  
* Gaussian: attributes are numeric, can assume from a gaussian distribution