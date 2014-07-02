AdaBoost
========

> Zhi-hua Zhou

### General Boosting Procedure

**Input**: Instance distribution ![\mathcal{D}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D); Base learning algorithm L; Number of learning rounds T.

**Process**:

1. ![\mathcal{D}_1=\mathcal{D}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_1%3D%5Cmathcal%7BD%7D)
2. for ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):
3.   ![h_t=L(\mathcal{D}_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3DL%28%5Cmathcal%7BD%7D_t%29)
4.   ![\epsilon_t=\mathrm{Pr}_{\boldsymbol{x}\sim\mathcal{D}_{t,y}}\boldsymbol{I}[h_t(\boldsymbol{x})\neq y]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7B%5Cboldsymbol%7Bx%7D%5Csim%5Cmathcal%7BD%7D_%7Bt%2Cy%7D%7D%5Cboldsymbol%7BI%7D%5Bh_t%28%5Cboldsymbol%7Bx%7D%29%5Cneq%20y%5D)
5.   ![\mathcal{D}_{t+1}=\mathrm{AdjustDistribution}(\mathcal{D}_t,\epsilon_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_%7Bt&plus;1%7D%3D%5Cmathrm%7BAdjustDistribution%7D%28%5Cmathcal%7BD%7D_t%2C%5Cepsilon_t%29)
6. **end**

**Output**: ![H(\boldsymbol{x})=\mathrm{CombineOutputs}(\{h_t(\boldsymbol{x})\})](http://latex.codecogs.com/gif.latex?%5Cbg_white%20H%28%5Cboldsymbol%7Bx%7D%29%3D%5Cmathrm%7BCombineOutputs%7D%28%5C%7Bh_t%28%5Cboldsymbol%7Bx%7D%29%5C%7D%29)

### AdaBoost

> Freud and Schapire

Given: ![(x_1,y_1),\dots,(x_m,y_m)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%28x_1%2Cy_1%29%2C%5Cdots%2C%28x_m%2Cy_m%29) where ![x_i\in{X},y_i\in{Y}=\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20x_i%5Cin%7BX%7D%2Cy_i%5Cin%7BY%7D%3D%5C%7B-1%2C&plus;1%5C%7D)

Initialize ![D_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_1%28i%29%3D1/m).

For ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):

- Train weak (base) learner using distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t).

- Get weak hypothesis ![h_t:X\rightarrow\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Crightarrow%5C%7B-1%2C&plus;1%5C%7D) with error ![\epsilon_t=\mathrm{Pr}_{i\sim D_i}[h_t(x_i)\neq y_i]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7Bi%5Csim%20D_i%7D%5Bh_t%28x_i%29%5Cneq%20y_i%5D).

- Choose ![\alpha_t=\frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t}\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha_t%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cleft%28%5Cfrac%7B1-%5Cepsilon_t%7D%7B%5Cepsilon_t%7D%5Cright%29).

- Update:

![\begin{align*}D_{t+1}(i)&=\frac{D_t(i)}{Z_t}\times\begin{cases}e^{-\alpha_t}\quad\textrm{if }h_t(x_i)=y_i\\e^{a_i}\quad\textrm{if }h_t(x_i)\neq y_i\end{cases}\\&=\frac{D_t(i)\exp(-\alpha_ty_ih_t(x_i))}{Z_t}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbegin%7Balign*%7DD_%7Bt&plus;1%7D%28i%29%26%3D%5Cfrac%7BD_t%28i%29%7D%7BZ_t%7D%5Ctimes%5Cbegin%7Bcases%7De%5E%7B-%5Calpha_t%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%3Dy_i%5C%5Ce%5E%7Ba_i%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%5Cneq%20y_i%5Cend%7Bcases%7D%5C%5C%26%3D%5Cfrac%7BD_t%28i%29%5Cexp%28-%5Calpha_ty_ih_t%28x_i%29%29%7D%7BZ_t%7D%5Cend%7Balign*%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization factor (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

Output the final hypthoses:

![H(x)=\mathrm{sign}\left(\sum_{t=1}^{T}\alpha_th_t(x)\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20H%28x%29%3D%5Cmathrm%7Bsign%7D%5Cleft%28%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Calpha_th_t%28x%29%5Cright%29).

> Trevor Hastie

Initialize the observation weights ![w_i=1/n, i=1,2,\cdots,n](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i%3D1/n%2C%20i%3D1%2C2%2C%5Ccdots%2Cn).

For ![m=1,2,\cdots,M](http://latex.codecogs.com/gif.latex?%5Cbg_white%20m%3D1%2C2%2C%5Ccdots%2CM):

- Fit a classifier ![T^{(m)}(\boldsymbol{x})](http://latex.codecogs.com/gif.latex?%5Cbg_white%20T%5E%7B%28m%29%7D%28%5Cboldsymbol%7Bx%7D%29) to the training data using weights ![w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i).

- Compute ![\mathrm{err}^{(m)}=\sum_{i=1}^{n}w_i\mathbb{I}(c_i\neq T^{m}(\boldsymbol{x}_i))/\sum_{i=1}^{n}w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7Dw_i%5Cmathbb%7BI%7D%28c_i%5Cneq%20T%5E%7Bm%7D%28%5Cboldsymbol%7Bx%7D_i%29%29/%5Csum_%7Bi%3D1%7D%5E%7Bn%7Dw_i).

- Compute ![\alpha^{(m)}=\log\frac{1-\mathrm{err}^{(m)}}{\mathrm{err}^{(m)}}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha%5E%7B%28m%29%7D%3D%5Clog%5Cfrac%7B1-%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%7D%7B%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%7D)

- Set ![w_i\leftarrow w_i\cdot\exp\Big(\alpha^{(m)}\cdot\mathbb{I}\big(c_i\neq T^{(m)}(\boldsymbol{x}_i)\big)\Big)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i%5Cleftarrow%20w_i%5Ccdot%5Cexp%5CBig%28%5Calpha%5E%7B%28m%29%7D%5Ccdot%5Cmathbb%7BI%7D%5Cbig%28c_i%5Cneq%20T%5E%7B%28m%29%7D%28%5Cboldsymbol%7Bx%7D_i%29%5Cbig%29%5CBig%29)

for ![i=1,2,\dots,n](http://latex.codecogs.com/gif.latex?%5Cbg_white%20i%3D1%2C2%2C%5Cdots%2Cn).

- Re-normalize ![w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i).

Output

![C(\boldsymbol{x})=\arg\max_k\sum_{m=1}^{M}\alpha^{(m)}\cdot\mathbb{I}(T^{(m)}(\boldsymbol{x})=k)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20C%28%5Cboldsymbol%7Bx%7D%29%3D%5Carg%5Cmax_k%5Csum_%7Bm%3D1%7D%5E%7BM%7D%5Calpha%5E%7B%28m%29%7D%5Ccdot%5Cmathbb%7BI%7D%28T%5E%7B%28m%29%7D%28%5Cboldsymbol%7Bx%7D%29%3Dk%29).

> Zhi-hua Zhou

**Input**: Dataset ![D=\{(\boldsymbol{x}_1,y_1),(\boldsymbol{x}_2,y_2),\dots,(\boldsymbol{x}_m,y_m)\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D%3D%5C%7B%28%5Cboldsymbol%7Bx%7D_1%2Cy_1%29%2C%28%5Cboldsymbol%7Bx%7D_2%2Cy_2%29%2C%5Cdots%2C%28%5Cboldsymbol%7Bx%7D_m%2Cy_m%29%5C%7D); Base learning algorithm L; Number of learning rounds T.

**Process**:

1. ![\mathcal{D}_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_1%28i%29%3D1/m)
2. **for** ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):
3.    ![h_t=L(D,\mathcal{D}_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3DL%28D%2C%5Cmathcal%7BD%7D_t%29)
4.    ![\epsilon_t=\mathrm{Pr}_{\boldsymbol{x}\sim\mathcal{D}_{t,y}}\boldsymbol{I}[h_t(\boldsymbol{x})\neq y]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7B%5Cboldsymbol%7Bx%7D%5Csim%5Cmathcal%7BD%7D_%7Bt%2Cy%7D%7D%5Cboldsymbol%7BI%7D%5Bh_t%28%5Cboldsymbol%7Bx%7D%29%5Cneq%20y%5D)
5.   **if** ![\epsilon_t>0.5](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3E0.5) **then break**
6. ![\alpha_t=\frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t} \right )](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha_t%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cleft%28%5Cfrac%7B1-%5Cepsilon_t%7D%7B%5Cepsilon_t%7D%20%5Cright%20%29)
