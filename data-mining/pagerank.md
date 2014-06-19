PageRank
========

### Define R(i)

How do we define the importance of a page (rank):

1. how many pages link to it (sum of pages)
2. is the page linking to it important (rank of that page)

Let

- R(i) be the rank of a page i
- N(i) be the number of pages which page i links to
- B(i) (back) be the set of pages which link to page i
- O(i) (out) be the set of pages which page i links to
- V (vertex) be the set of all pages
- E (edge) be the set of links in the form of (i, j)
- n be the total number of pages

then

![R(i)=\sum_{j\in B(i)} R(j)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%28i%29%3D%5Csum_%7Bj%5Cin%20B%28i%29%7D%20R%28j%29)

To decrease the importance of a page with multiple links, divide it by the number of pages it links to

![R(i)=\sum_{j\in B(i)} \frac{R(j)}{N(j)}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%28i%29%3D%5Csum_%7Bj%5Cin%20B%28i%29%7D%20%5Cfrac%7BR%28j%29%7D%7BN%28j%29%7D)

To normalize the rank, add a constant c

![R(i)=c\sum_{j\in B(i)} \frac{R(j)}{N(j)}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%28i%29%3Dc%5Csum_%7Bj%5Cin%20B%28i%29%7D%20%5Cfrac%7BR%28j%29%7D%7BN%28j%29%7D)

which is equivalent to the formula given in the paper

![R(u)=c\sum_{v\in B_u}\frac{R(v)}{N_v}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%28u%29%3Dc%5Csum_%7Bv%5Cin%20B_u%7D%5Cfrac%7BR%28v%29%7D%7BN_v%7D)

### Calculate R(i)

Let matrix A denote the adjacency matrix of all pages, where Aij corresponds to the link from page i to page j. Let Aij equal 1 divided by the number of pages which page i links to, which is

![A_{ij}=\begin{cases}\frac{1}{O_i}&\textrm{if }(i,j)\in E\\0&\textrm{otherwise}\end{cases}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20A_%7Bij%7D%3D%5Cbegin%7Bcases%7D%5Cfrac%7B1%7D%7BO_i%7D%26%5Ctextrm%7Bif%20%7D%28i%2Cj%29%5Cin%20E%5C%5C0%26%5Ctextrm%7Botherwise%7D%5Cend%7Bcases%7D)

Let R be an n-dimensional column vector of ranks

![R=(R(1),R(2),\dots,R(n))^T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%3D%28R%281%29%2CR%282%29%2C%5Cdots%2CR%28n%29%29%5ET)

then the equation is equal to

![R=A^TR](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%3DA%5ETR)

Recall the eigenvalue and eigenvector in linear algebra

![Ax=\lambda x](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Ax%3D%5Clambda%20x)

where λ is the eigenvalue and the solution of x (in our case R) is the eigenvector. Thus for the equation

![R=cA^TR](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%3DcA%5ETR)

which equals to

![\frac{1}{c}R=A^TR](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cfrac%7B1%7D%7Bc%7DR%3DA%5ETR)

R is the eigenvector of A with eigenvalue equals to 1/c.

We use **power iteration** to get the value of R.

### Power Iteration

A must satisfy two conditions such that 1 is the largest eigenvalue and R is the *principal eigenvector*:

1. A is a stochastic matrix
2. A is irreducible
3. A is aperiodic

A **stochastic** matrix is the transition matrix for a finite Markov chain whose entries in each row are nonnegative real numbers and sum to 1. This requires that every Web page must have at least one out-link. In fact there are *dangling pages* which have no out-links, reflected in transition matrix A by some rows of complete 0's.

Fix this problem by adding a complete set of outgoing links from each such page i to all the pages (let Aij be 1/n).

A **irreducible** matrix means the graph is strongly connected, which exists if and only if for each pair of node u, v in V, there is a path from u to v.

A **aperiodic** means if all states are aperiodic. [Omit the definition of periodic of a Markov chain state]

Example of periodic state:

![A=\begin{bmatrix}0&1&0\\0&0&1\\1&0&0\end{bmatrix}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20A%3D%5Cbegin%7Bbmatrix%7D0%261%260%5C%5C0%260%261%5C%5C1%260%260%5Cend%7Bbmatrix%7D)

which is a periodic Markov chain with k = 3.

Fix these two problems by adding a link from each page to every page and give each link a small transition probability controlled by a parameter d.

The augmented transition matrix becomes irreducible and also aperiodic

![R=\left((1-d)\frac{E}{n}+dA^T \right )R](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%3D%5Cleft%28%281-d%29%5Cfrac%7BE%7D%7Bn%7D&plus;dA%5ET%20%5Cright%20%29R)

where E is an nxn square matrix of all 1's. Assume that A is already an stochastic matrix, then

![R=(1-d)e+dA^TR](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%3D%281-d%29e&plus;dA%5ETR)

![R(i)=(1-d)+d\sum_{j=1}^{n}A_{ji}R(j)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%28i%29%3D%281-d%29&plus;d%5Csum_%7Bj%3D1%7D%5E%7Bn%7DA_%7Bji%7DR%28j%29)

which is equivalent to the formula given in the paper

![R'(u)=c\sum_{v\in B_u}\frac{R'(v)}{N_v}+cE(u)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%27%28u%29%3Dc%5Csum_%7Bv%5Cin%20B_u%7D%5Cfrac%7BR%27%28v%29%7D%7BN_v%7D&plus;cE%28u%29)

such that c is maximized and ![\|R'\|_1=1](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5C%7CR%27%5C%7C_1%3D1)

In matrix denotation

![R'=c(AR'+E)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%27%3Dc%28AR%27&plus;E%29)

which we can rewrite as

![R'=c(A+E\times 1)R'](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R%27%3Dc%28A&plus;E%5Ctimes%201%29R%27)

where 1 is the vector consisting of all ones and R is an eigenvector of (A+Ex1).

In the Google patent, the formula is

![r(A)=\frac{\alpha}{N}+(1-\alpha)\left(\frac{r(B_1)}{|B_1|}+\cdots+\frac{r(B_n)}{|B_n|}\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20r%28A%29%3D%5Cfrac%7B%5Calpha%7D%7BN%7D&plus;%281-%5Calpha%29%5Cleft%28%5Cfrac%7Br%28B_1%29%7D%7B%7CB_1%7C%7D&plus;%5Ccdots&plus;%5Cfrac%7Br%28B_n%29%7D%7B%7CB_n%7C%7D%20%5Cright%20%29)

### Compute PageRank

Let S be almost any vector over Web pages (for example E)

![R_0\leftarrow S](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R_0%5Cleftarrow%20S)

Loop:

![R_i+1\leftarrow AR_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R_i&plus;1%5Cleftarrow%20AR_i)

![d\leftarrow \|R_i\|_1-\|R_{i+1}\|_1](http://latex.codecogs.com/gif.latex?%5Cbg_white%20d%5Cleftarrow%20%5C%7CR_i%5C%7C_1-%5C%7CR_%7Bi&plus;1%7D%5C%7C_1)

![R_{i+1}\leftarrow R_{i+1}+dE](http://latex.codecogs.com/gif.latex?%5Cbg_white%20R_%7Bi&plus;1%7D%5Cleftarrow%20R_%7Bi&plus;1%7D&plus;dE)

![\delta\leftarrow\|R_{i+1}-R_i\|_1](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cdelta%5Cleftarrow%5C%7CR_%7Bi&plus;1%7D-R_i%5C%7C_1)

while ![\delta>\epsilon](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cdelta%3E%5Cepsilon)

