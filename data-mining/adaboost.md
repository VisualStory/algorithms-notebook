AdaBoost
========

> Zhi-hua Zhou

### General Boosting Procedure

**Input**: Instance distribution ![\mathcal{D}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D); Base learning algorithm L; Number of learning rounds T.

**Process**:

1 ![\mathcal{D}_1=\mathcal{D}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_1%3D%5Cmathcal%7BD%7D)

2 **for** ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):

3   ![h_t=L(\mathcal{D}_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3DL%28%5Cmathcal%7BD%7D_t%29)

4   ![\epsilon_t=\mathrm{Pr}_{\boldsymbol{x}\sim\mathcal{D}_{t,y}}\boldsymbol{I}[h_t(\boldsymbol{x})\neq y]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7B%5Cboldsymbol%7Bx%7D%5Csim%5Cmathcal%7BD%7D_%7Bt%2Cy%7D%7D%5Cboldsymbol%7BI%7D%5Bh_t%28%5Cboldsymbol%7Bx%7D%29%5Cneq%20y%5D)

5   ![\mathcal{D}_{t+1}=\mathrm{AdjustDistribution}(\mathcal{D}_t,\epsilon_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_%7Bt&plus;1%7D%3D%5Cmathrm%7BAdjustDistribution%7D%28%5Cmathcal%7BD%7D_t%2C%5Cepsilon_t%29)

6 **end**

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

1 ![\mathcal{D}_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathcal%7BD%7D_1%28i%29%3D1/m)

2 **for** ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):

3    ![h_t=L(D,\mathcal{D}_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3DL%28D%2C%5Cmathcal%7BD%7D_t%29)

4    ![\epsilon_t=\mathrm{Pr}_{\boldsymbol{x}\sim\mathcal{D}_{t,y}}\boldsymbol{I}[h_t(\boldsymbol{x})\neq y]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7B%5Cboldsymbol%7Bx%7D%5Csim%5Cmathcal%7BD%7D_%7Bt%2Cy%7D%7D%5Cboldsymbol%7BI%7D%5Bh_t%28%5Cboldsymbol%7Bx%7D%29%5Cneq%20y%5D)

5   **if** ![\epsilon_t>0.5](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3E0.5) **then break**

6 ![\alpha_t=\frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t} \right )](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha_t%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cleft%28%5Cfrac%7B1-%5Cepsilon_t%7D%7B%5Cepsilon_t%7D%20%5Cright%20%29)

7 ![\begin{align*}\mathcal{D}_{t+1}(i)&=\frac{\mathcal{D}_t(i)}{Z_t}\times\begin{cases}\exp(-\alpha_t)\textrm{ if }h_t(\boldsymbol{x}_i)= y_i\\\exp(\alpha_t)\textrm{ if }h_t(\boldsymbol{x}_i)\neq y_i\end{cases}\\&=\frac{\mathcal{D}_t(i)\exp(-\alpha_ty_ih_t(\boldsymbol{x_i}))}{Z_t}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbegin%7Balign*%7D%5Cmathcal%7BD%7D_%7Bt&plus;1%7D%28i%29%26%3D%5Cfrac%7B%5Cmathcal%7BD%7D_t%28i%29%7D%7BZ_t%7D%5Ctimes%5Cbegin%7Bcases%7D%5Cexp%28-%5Calpha_t%29%5Ctextrm%7B%20if%20%7Dh_t%28%5Cboldsymbol%7Bx%7D_i%29%3D%20y_i%5C%5C%5Cexp%28%5Calpha_t%29%5Ctextrm%7B%20if%20%7Dh_t%28%5Cboldsymbol%7Bx%7D_i%29%5Cneq%20y_i%5Cend%7Bcases%7D%5C%5C%26%3D%5Cfrac%7B%5Cmathcal%7BD%7D_t%28i%29%5Cexp%28-%5Calpha_ty_ih_t%28%5Cboldsymbol%7Bx_i%7D%29%29%7D%7BZ_t%7D%5Cend%7Balign*%7D)

8 **end**

**Output**: ![H(\boldsymbol{x})=\mathrm{sign}(\sum_{t=1}^{T}\alpha_th_t(\boldsymbol{x}))](http://latex.codecogs.com/gif.latex?%5Cbg_white%20H%28%5Cboldsymbol%7Bx%7D%29%3D%5Cmathrm%7Bsign%7D%28%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Calpha_th_t%28%5Cboldsymbol%7Bx%7D%29%29)

### Algorithm AdaBoost.M1

**Input**

- sequence of m examples ![\langle(x_1,y_1),\dots,(x_m,y_m)\rangle](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Clangle%28x_1%2Cy_1%29%2C%5Cdots%2C%28x_m%2Cy_m%29%5Crangle) with labels ![y_i\in Y=\{1,\dots,k\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20y_i%5Cin%20Y%3D%5C%7B1%2C%5Cdots%2Ck%5C%7D)
- weak learning algorithm **WeakLearn**
- integer T sepecifying number of iterations

**Initialize** ![D_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_1%28i%29%3D1/m) for all i.

**Do for** ![t=1,2,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C2%2C%5Cdots%2CT)

1 Call **WeakLearn**, providing it with the distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t)

2 Get back a hypothesis ![h_t:X\rightarrow Y](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Crightarrow%20Y)

3 Calculate the error of ![h_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t): ![\epsilon_t=\sum_{i:h_t(x_i)\neq y_i}D_t(i)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Csum_%7Bi%3Ah_t%28x_i%29%5Cneq%20y_i%7DD_t%28i%29). If ![\epsilon_t>1/2](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3E1/2), then set ![T=t-1](http://latex.codecogs.com/gif.latex?%5Cbg_white%20T%3Dt-1) and abort loop

4 Set ![\beta_t=\epsilon_t/(1-\epsilon_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbeta_t%3D%5Cepsilon_t/%281-%5Cepsilon_t%29).

5 Update distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t): ![D_{t+1}(i)=\frac{D_t(i)}{Z_t}\times\begin{cases}\beta_t&\textrm{if }h_t(x_t)=y_t\\1&\textrm{otherwise}\end{cases}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D%28i%29%3D%5Cfrac%7BD_t%28i%29%7D%7BZ_t%7D%5Ctimes%5Cbegin%7Bcases%7D%5Cbeta_t%26%5Ctextrm%7Bif%20%7Dh_t%28x_t%29%3Dy_t%5C%5C1%26%5Ctextrm%7Botherwise%7D%5Cend%7Bcases%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization constant (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

**Output** the final hypothesis: ![h_{fin}(x)=\arg\max_{y\in Y}\sum_{t:h_t(x)=y}\log\frac{1}{\beta_t}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_%7Bfin%7D%28x%29%3D%5Carg%5Cmax_%7By%5Cin%20Y%7D%5Csum_%7Bt%3Ah_t%28x%29%3Dy%7D%5Clog%5Cfrac%7B1%7D%7B%5Cbeta_t%7D)

### Algorithm AdaBoost.M2

**Input**

- sequence of m examples ![\langle(x_1,y_1),\dots,(x_m,y_m)\rangle](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Clangle%28x_1%2Cy_1%29%2C%5Cdots%2C%28x_m%2Cy_m%29%5Crangle) with labels ![y_i\in Y=\{1,\dots,k\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20y_i%5Cin%20Y%3D%5C%7B1%2C%5Cdots%2Ck%5C%7D)
- weak learning algorithm **WeakLearn**
- integer T sepecifying number of iterations

Let ![B=\{(i,y):i\in \{1,\dots,m\},y\neq y_i\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20B%3D%5C%7B%28i%2Cy%29%3Ai%5Cin%20%5C%7B1%2C%5Cdots%2Cm%5C%7D%2Cy%5Cneq%20y_i%5C%7D)

**Initialize** ![D_1(i,y)=1/|B|\textrm{ for }(i,y)\in B](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_1%28i%2Cy%29%3D1/%7CB%7C%5Ctextrm%7B%20for%20%7D%28i%2Cy%29%5Cin%20B)

**Do for** ![t=1,2,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C2%2C%5Cdots%2CT)

1 Call **WeakLearn**, providing it with mislabel distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t)

2 Get back a hypothesis ![h_t:X\times Y\rightarrow[0,1](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Ctimes%20Y%5Crightarrow%5B0%2C1%5D)

3 Calculate the pseudo-loss of ![h_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t): ![\epsilon_t=\frac{1}{2}\sum_{(i,y)\in B}D_t(i,y)(1-h_t(x_i,y_i)+h_t(x_i,y))](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cfrac%7B1%7D%7B2%7D%5Csum_%7B%28i%2Cy%29%5Cin%20B%7DD_t%28i%2Cy%29%281-h_t%28x_i%2Cy_i%29&plus;h_t%28x_i%2Cy%29%29).

4 Set ![\beta_t=\epsilon_t/(1-\epsilon_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbeta_t%3D%5Cepsilon_t/%281-%5Cepsilon_t%29).

5 Update distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t): ![D_{t+!}(i,y)=\frac{D_t(i,y)}{Z_t}\cdot\beta^{(1/2)(1+h_t(x_i,y_i)-h_t(x_i,y))}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;%21%7D%28i%2Cy%29%3D%5Cfrac%7BD_t%28i%2Cy%29%7D%7BZ_t%7D%5Ccdot%5Cbeta%5E%7B%281/2%29%281&plus;h_t%28x_i%2Cy_i%29-h_t%28x_i%2Cy%29%29%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization constant (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

**Output** the hypothesis: ![h_{fin}(x)=\arg\max_{y\in Y}\sum_{t=1}^{T}\left(\log\frac{1}{\beta_t}\right)h_t(x,y)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_%7Bfin%7D%28x%29%3D%5Carg%5Cmax_%7By%5Cin%20Y%7D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Cleft%28%5Clog%5Cfrac%7B1%7D%7B%5Cbeta_t%7D%5Cright%29h_t%28x%2Cy%29).
