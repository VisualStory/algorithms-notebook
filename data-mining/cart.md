Classification and Regression Tree
==================================

### Implementations

- R pakcages
  - {rpart}
  - {tree}
  - {party}
  
### Notations

![\pi_i](http://latex.codecogs.com/gif.latex?%5Cpi_i): prior probabilities of each class

![L(i,j)](http://latex.codecogs.com/gif.latex?L%28i%2Cj%29): loss functions

![\tau(x)](http://latex.codecogs.com/gif.latex?%5Ctau%28x%29): true class of an observation x, where x is the vector of predictor variables.

![\tau(A)](http://latex.codecogs.com/gif.latex?%5Ctau%28A%29): the class assigned to A, if A were to be taken as a final node.

![n_i,n_A](http://latex.codecogs.com/gif.latex?n_i%2Cn_A): number of obeservations in the sample that are class i, in node A, respectively

![n_{iA}](http://latex.codecogs.com/gif.latex?n_%7BiA%7D): number of observations in the sample that are class i and node A

![\begin{align*}P(A)&=\sum_{i=1}^{C}\pi_iP\{x\in{A}|\tau(x)=i\}\\&\approx\sum_{i=1}^{C}\pi_i\frac{n_{iA}}{n_i}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DP%28A%29%26%3D%5Csum_%7Bi%3D1%7D%5E%7BC%7D%5Cpi_iP%5C%7Bx%5Cin%7BA%7D%7C%5Ctau%28x%29%3Di%5C%7D%5C%5C%26%5Capprox%5Csum_%7Bi%3D1%7D%5E%7BC%7D%5Cpi_i%5Cfrac%7Bn_%7BiA%7D%7D%7Bn_i%7D%5Cend%7Balign*%7D): Probability of A (for future observations)

![\begin{align*}P(i|A)&=\pi_i\frac{P\{x\in{A}|\tau(x)\}}{P\{x\in{A}\}}\\&\approx\pi_i\frac{n_{iA}/n_i}{\sum\pi_i(n_{iA}/n_i)}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DP%28i%7CA%29%26%3D%5Cpi_i%5Cfrac%7BP%5C%7Bx%5Cin%7BA%7D%7C%5Ctau%28x%29%5C%7D%7D%7BP%5C%7Bx%5Cin%7BA%7D%5C%7D%7D%5C%5C%26%5Capprox%5Cpi_i%5Cfrac%7Bn_%7BiA%7D/n_i%7D%7B%5Csum%5Cpi_i%28n_%7BiA%7D/n_i%29%7D%5Cend%7Balign*%7D): ![P\{\tau(x)=i|x\in{A}\}](http://latex.codecogs.com/gif.latex?P%5C%7B%5Ctau%28x%29%3Di%7Cx%5Cin%7BA%7D%5C%7D) (for future observations)

![R(A)=\sum_{i=1}^{C}p(i|A)L(i,\tau(A))](http://latex.codecogs.com/gif.latex?R%28A%29%3D%5Csum_%7Bi%3D1%7D%5E%7BC%7Dp%28i%7CA%29L%28i%2C%5Ctau%28A%29%29): risk of A, where ![\tau(A)](http://latex.codecogs.com/gif.latex?%5Ctau%28A%29) is chosen to minimize this risk.

![R(T)=\sum_{j=1}^{k}P(A_j)R(A_j)](http://latex.codecogs.com/gif.latex?R%28T%29%3D%5Csum_%7Bj%3D1%7D%5E%7Bk%7DP%28A_j%29R%28A_j%29): risk of a model (or tree) T, where ![A_j](http://latex.codecogs.com/gif.latex?A_j) are the terminal nodes of the tree.

### Formulas

