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

![\tau(x)](http://latex.codecogs.com/gif.latex?%5Ctau%28x%29): true class of an observation x, where x is the vector of predictor variables

![\tau(A)](http://latex.codecogs.com/gif.latex?%5Ctau%28A%29): the class assigned to A, if A were to be taken as a final node

![n_i,n_A](http://latex.codecogs.com/gif.latex?n_i%2Cn_A): number of obeservations in the sample that are class i, in node A, respectively

![n_{iA}](http://latex.codecogs.com/gif.latex?n_%7BiA%7D): number of observations in the sample that are class i and node A

![\begin{align*}P(A)&=\sum_{i=1}^{C}\pi_iP\{x\in{A}|\tau(x)=i\}\\&\approx\sum_{i=1}^{C}\pi_i\frac{n_{iA}}{n_i}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DP%28A%29%26%3D%5Csum_%7Bi%3D1%7D%5E%7BC%7D%5Cpi_iP%5C%7Bx%5Cin%7BA%7D%7C%5Ctau%28x%29%3Di%5C%7D%5C%5C%26%5Capprox%5Csum_%7Bi%3D1%7D%5E%7BC%7D%5Cpi_i%5Cfrac%7Bn_%7BiA%7D%7D%7Bn_i%7D%5Cend%7Balign*%7D): Probability of A (for future observations)

![\begin{align*}P(i|A)&=\pi_i\frac{P\{x\in{A}|\tau(x)\}}{P\{x\in{A}\}}\\&\approx\pi_i\frac{n_{iA}/n_i}{\sum\pi_i(n_{iA}/n_i)}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DP%28i%7CA%29%26%3D%5Cpi_i%5Cfrac%7BP%5C%7Bx%5Cin%7BA%7D%7C%5Ctau%28x%29%5C%7D%7D%7BP%5C%7Bx%5Cin%7BA%7D%5C%7D%7D%5C%5C%26%5Capprox%5Cpi_i%5Cfrac%7Bn_%7BiA%7D/n_i%7D%7B%5Csum%5Cpi_i%28n_%7BiA%7D/n_i%29%7D%5Cend%7Balign*%7D): ![P\{\tau(x)=i|x\in{A}\}](http://latex.codecogs.com/gif.latex?P%5C%7B%5Ctau%28x%29%3Di%7Cx%5Cin%7BA%7D%5C%7D) (for future observations)

![R(A)=\sum_{i=1}^{C}p(i|A)L(i,\tau(A))](http://latex.codecogs.com/gif.latex?R%28A%29%3D%5Csum_%7Bi%3D1%7D%5E%7BC%7Dp%28i%7CA%29L%28i%2C%5Ctau%28A%29%29): risk of A, where ![\tau(A)](http://latex.codecogs.com/gif.latex?%5Ctau%28A%29) is chosen to minimize this risk

![R(T)=\sum_{j=1}^{k}P(A_j)R(A_j)](http://latex.codecogs.com/gif.latex?R%28T%29%3D%5Csum_%7Bj%3D1%7D%5E%7Bk%7DP%28A_j%29R%28A_j%29): risk of a model (or tree) T, where ![A_j](http://latex.codecogs.com/gif.latex?A_j) are the terminal nodes of the tree

## Formulas

### Splitting Criteria (Risk)

![P(A_L)R(A_L)+P(A_R)R(A_R)\leq{P(A)R(A)}](http://latex.codecogs.com/gif.latex?P%28A_L%29R%28A_L%29&plus;P%28A_R%29R%28A_R%29%5Cleq%7BP%28A%29R%28A%29%7D): split a node A into two sons AL and AR (left and right sons)

2 problems with one obvious way to build a tree by choosing a split that maximize ΔR, the decrease in risk.

1. sometimes minimum risk prediction will not solve the majority problem in the first few splits
2. risk reduction is linear, which is not friendly to splits afterwards

Instead of using risk functions to choose splits, CART uses a impurity function of a node.

### Impurity Function

![I(A)=\sum_{i=1}^{C}f(p_{iA})](http://latex.codecogs.com/gif.latex?I%28A%29%3D%5Csum_%7Bi%3D1%7D%5E%7BC%7Df%28p_%7BiA%7D%29), where piA is the proportion of those in A that belong toclassifor future samples.

![\Delta{I}=p(A)I(A)-p(A_L)I(A_L)-p(A_R)I(A_R)](http://latex.codecogs.com/gif.latex?%5CDelta%7BI%7D%3Dp%28A%29I%28A%29-p%28A_L%29I%28A_L%29-p%28A_R%29I%28A_R%29) should be maximized by choosing a suitable split.

There are 2 impurity functions:

1. Information Entropy
2. Gini Index

### Entropy

![\begin{align*}H(X)&=-p_1\log_2p_1-p_2\log_2p_2-\cdots-p_m\log_2p_m\\&=-\sum_{i=1}^mp_i\log_2p_i\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7DH%28X%29%26%3D-p_1%5Clog_2p_1-p_2%5Clog_2p_2-%5Ccdots-p_m%5Clog_2p_m%5C%5C%26%3D-%5Csum_%7Bi%3D1%7D%5Emp_i%5Clog_2p_i%5Cend%7Balign*%7D)

### Conditional Entropy

![H(Y|X)=-\sum_{i=1}^mp(X=v_i)H(Y|X=v_i)](http://latex.codecogs.com/gif.latex?H%28Y%7CX%29%3D-%5Csum_%7Bi%3D1%7D%5Emp%28X%3Dv_i%29H%28Y%7CX%3Dv_i%29) where ![X\in\{v_1,v_2,\cdots,v_m\}](http://latex.codecogs.com/gif.latex?X%5Cin%5C%7Bv_1%2Cv_2%2C%5Ccdots%2Cv_m%5C%7D)

### Information Gain

![IG(Y|X)=H(Y)-H(Y|X)](http://latex.codecogs.com/gif.latex?IG%28Y%7CX%29%3DH%28Y%29-H%28Y%7CX%29)

![Gain(S,A)=Entropy(S)-\sum_{v\in{Values(A)}}\frac{|S_v|}{|S|}](http://latex.codecogs.com/gif.latex?Gain%28S%2CA%29%3DEntropy%28S%29-%5Csum_%7Bv%5Cin%7BValues%28A%29%7D%7D%5Cfrac%7B%7CS_v%7C%7D%7B%7CS%7C%7D) where S is samples and A is an attribute.

### Gini Index

![Gini(X)=1-\sum_{i=1}^{m}p_i^2](http://latex.codecogs.com/gif.latex?Gini%28X%29%3D1-%5Csum_%7Bi%3D1%7D%5E%7Bm%7Dp_i%5E2)

![Gini(X)=\sum_i\sum_{j\neq{i}}p_ip_j=\sum_i\sum_jp_ip_j-\sum_ip_i^2=1-\sum_ip_i^2](http://latex.codecogs.com/gif.latex?Gini%28X%29%3D%5Csum_i%5Csum_%7Bj%5Cneq%7Bi%7D%7Dp_ip_j%3D%5Csum_i%5Csum_jp_ip_j-%5Csum_ip_i%5E2%3D1-%5Csum_ip_i%5E2)

### Generalized Gini Index

![G(p)=\sum_i\sum_jL(i,j)p_ip_j](http://latex.codecogs.com/gif.latex?G%28p%29%3D%5Csum_i%5Csum_jL%28i%2Cj%29p_ip_j)

## Cost Complexity Pruning

![R(T)=\sum_{i=1}^kp(T_i)R(T_i)](http://latex.codecogs.com/gif.latex?R%28T%29%3D%5Csum_%7Bi%3D1%7D%5Ekp%28T_i%29R%28T_i%29) where T1, T2, ..., Tk are terminal nodes of a Tree T and |T| is the number of terminal nodes.

### Cost for the Tree

![R_\alpha(T)=R(T)+\alpha|T|](http://latex.codecogs.com/gif.latex?R_%5Calpha%28T%29%3DR%28T%29&plus;%5Calpha%7CT%7C)

### Complexity Parameter

![R_{cp}(T)\equiv R(T)+cp*|T|*R(T_0)](http://latex.codecogs.com/gif.latex?R_%7Bcp%7D%28T%29%5Cequiv%20R%28T%29&plus;cp*%7CT%7C*R%28T_0%29)

*Reference*

L. Breiman, J.H. Friedman, R.A. Olshen, and C.J. Stone. Classification and Regression Trees. Wadsworth, Belmont, Ca, 1983.
