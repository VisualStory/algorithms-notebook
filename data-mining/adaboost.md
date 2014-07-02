AdaBoost
========

### Boosting

> Schapire

Given: ![(x_1,y_1),\dots,(x_m,y_m)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%28x_1%2Cy_1%29%2C%5Cdots%2C%28x_m%2Cy_m%29) where ![x_i\in{X},y_i\in{Y}=\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20x_i%5Cin%7BX%7D%2Cy_i%5Cin%7BY%7D%3D%5C%7B-1%2C&plus;1%5C%7D)

Initialize ![D_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_1%28i%29%3D1/m)

For ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):

- Train weak learner using distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t)

- Get weak hypothesis ![h_t:X\rightarrow\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Crightarrow%5C%7B-1%2C&plus;1%5C%7D) with error

![\epsilon_t=\mathrm{Pr}_{i\sim D_i}[h_t(x_i)\neq y_i]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7Bi%5Csim%20D_i%7D%5Bh_t%28x_i%29%5Cneq%20y_i%5D).

- Choose ![\alpha_t=\frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t}\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha_t%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cleft%28%5Cfrac%7B1-%5Cepsilon_t%7D%7B%5Cepsilon_t%7D%5Cright%29)

- Update:

![\begin{align*}D_{t+1}(i)&=\frac{D_t(i)}{Z_t}\times\begin{cases}e^{-\alpha_t}\quad\textrm{if }h_t(x_i)=y_i\\e^{a_i}\quad\textrm{if }h_t(x_i)\neq y_i\end{cases}\\&=\frac{D_t(i)\exp(-\alpha_ty_ih_t(x_i))}{Z_t}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbegin%7Balign*%7DD_%7Bt&plus;1%7D%28i%29%26%3D%5Cfrac%7BD_t%28i%29%7D%7BZ_t%7D%5Ctimes%5Cbegin%7Bcases%7De%5E%7B-%5Calpha_t%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%3Dy_i%5C%5Ce%5E%7Ba_i%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%5Cneq%20y_i%5Cend%7Bcases%7D%5C%5C%26%3D%5Cfrac%7BD_t%28i%29%5Cexp%28-%5Calpha_ty_ih_t%28x_i%29%29%7D%7BZ_t%7D%5Cend%7Balign*%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization factor (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

Output the final hypthoses:

![H(x)=\mathrm{sign}\left(\sum_{t=1}^{T}\alpha_th_t(x)\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20H%28x%29%3D%5Cmathrm%7Bsign%7D%5Cleft%28%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Calpha_th_t%28x%29%5Cright%29).

---

