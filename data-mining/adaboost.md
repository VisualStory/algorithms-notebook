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

**Given**: ![(x_1,y_1),\dots,(x_m,y_m)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%28x_1%2Cy_1%29%2C%5Cdots%2C%28x_m%2Cy_m%29) where ![x_i\in{X},y_i\in{Y}=\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20x_i%5Cin%7BX%7D%2Cy_i%5Cin%7BY%7D%3D%5C%7B-1%2C&plus;1%5C%7D)

**Initialize** ![D_1(i)=1/m](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_1%28i%29%3D1/m).

For ![t=1,\dots,T](http://latex.codecogs.com/gif.latex?%5Cbg_white%20t%3D1%2C%5Cdots%2CT):

1 Train weak (base) learner using distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t).

2 Get weak hypothesis ![h_t:X\rightarrow\{-1,+1\}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Crightarrow%5C%7B-1%2C&plus;1%5C%7D) with error ![\epsilon_t=\mathrm{Pr}_{i\sim D_i}[h_t(x_i)\neq y_i]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cmathrm%7BPr%7D_%7Bi%5Csim%20D_i%7D%5Bh_t%28x_i%29%5Cneq%20y_i%5D).

3 Choose ![\alpha_t=\frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t}\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha_t%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cleft%28%5Cfrac%7B1-%5Cepsilon_t%7D%7B%5Cepsilon_t%7D%5Cright%29).

4 Update:

![\begin{align*}D_{t+1}(i)&=\frac{D_t(i)}{Z_t}\times\begin{cases}e^{-\alpha_t}\quad\textrm{if }h_t(x_i)=y_i\\e^{a_i}\quad\textrm{if }h_t(x_i)\neq y_i\end{cases}\\&=\frac{D_t(i)\exp(-\alpha_ty_ih_t(x_i))}{Z_t}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbegin%7Balign*%7DD_%7Bt&plus;1%7D%28i%29%26%3D%5Cfrac%7BD_t%28i%29%7D%7BZ_t%7D%5Ctimes%5Cbegin%7Bcases%7De%5E%7B-%5Calpha_t%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%3Dy_i%5C%5Ce%5E%7Ba_i%7D%5Cquad%5Ctextrm%7Bif%20%7Dh_t%28x_i%29%5Cneq%20y_i%5Cend%7Bcases%7D%5C%5C%26%3D%5Cfrac%7BD_t%28i%29%5Cexp%28-%5Calpha_ty_ih_t%28x_i%29%29%7D%7BZ_t%7D%5Cend%7Balign*%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization factor (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

**Output** the final hypthoses:

![H(x)=\mathrm{sign}\left(\sum_{t=1}^{T}\alpha_th_t(x)\right)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20H%28x%29%3D%5Cmathrm%7Bsign%7D%5Cleft%28%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Calpha_th_t%28x%29%5Cright%29).

> Trevor Hastie

**Initialize** the observation weights ![w_i=1/n, i=1,2,\cdots,n](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i%3D1/n%2C%20i%3D1%2C2%2C%5Ccdots%2Cn).

For ![m=1,2,\cdots,M](http://latex.codecogs.com/gif.latex?%5Cbg_white%20m%3D1%2C2%2C%5Ccdots%2CM):

1 Fit a classifier ![T^{(m)}(\boldsymbol{x})](http://latex.codecogs.com/gif.latex?%5Cbg_white%20T%5E%7B%28m%29%7D%28%5Cboldsymbol%7Bx%7D%29) to the training data using weights ![w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i).

2 Compute ![\mathrm{err}^{(m)}=\sum_{i=1}^{n}w_i\mathbb{I}(c_i\neq T^{m}(\boldsymbol{x}_i))/\sum_{i=1}^{n}w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7Dw_i%5Cmathbb%7BI%7D%28c_i%5Cneq%20T%5E%7Bm%7D%28%5Cboldsymbol%7Bx%7D_i%29%29/%5Csum_%7Bi%3D1%7D%5E%7Bn%7Dw_i).

3 Compute ![\alpha^{(m)}=\log\frac{1-\mathrm{err}^{(m)}}{\mathrm{err}^{(m)}}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Calpha%5E%7B%28m%29%7D%3D%5Clog%5Cfrac%7B1-%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%7D%7B%5Cmathrm%7Berr%7D%5E%7B%28m%29%7D%7D)

4 Set ![w_i\leftarrow w_i\cdot\exp\Big(\alpha^{(m)}\cdot\mathbb{I}\big(c_i\neq T^{(m)}(\boldsymbol{x}_i)\big)\Big)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i%5Cleftarrow%20w_i%5Ccdot%5Cexp%5CBig%28%5Calpha%5E%7B%28m%29%7D%5Ccdot%5Cmathbb%7BI%7D%5Cbig%28c_i%5Cneq%20T%5E%7B%28m%29%7D%28%5Cboldsymbol%7Bx%7D_i%29%5Cbig%29%5CBig%29)

for ![i=1,2,\dots,n](http://latex.codecogs.com/gif.latex?%5Cbg_white%20i%3D1%2C2%2C%5Cdots%2Cn).

5 Re-normalize ![w_i](http://latex.codecogs.com/gif.latex?%5Cbg_white%20w_i).

**Output**:

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

#### Proof

AdaBoost generates a sequence of hypotheses and combines them with weights, which can be regarded as anadditive weighted combination in the form of 

![H(x)=\sum_{t=1}^{T}\alpha_th_t(x)](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20H%28x%29%3D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Calpha_th_t%28x%29).

From this view, AdaBoost actually solves two problems, that is, how to generate the hypothesesht’s and how to determine the proper weights ![\alpha_t](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20%5Calpha_t)’s.

In order to have a highly efficient error reduction process, we try to minimize an exponential loss

![loss_{\exp}(h)=\mathbb{E}_{x\sim\mathcal{D},y}[e^{-yh(x)}]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20loss_%7B%5Cexp%7D%28h%29%3D%5Cmathbb%7BE%7D_%7Bx%5Csim%5Cmathcal%7BD%7D%2Cy%7D%5Be%5E%7B-yh%28x%29%7D%5D)

where ![yh(x)](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20yh%28x%29) is called as the **classification margin** of the hypothesis.

Suppose a set of hypotheses as well as their weights have already been obtained, and let H denote the combined hypothesis. Now, one more hypothesis h will be generated and is to be combined with H to form H+αh. The loss after the combination will be

![loss_{\exp}(H+\alpha h)=\mathbb{E}_{x\sim\mathcal{D},y}[e^{-y(H(x)+\alpha h(x))}]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20loss_%7B%5Cexp%7D%28H&plus;%5Calpha%20h%29%3D%5Cmathbb%7BE%7D_%7Bx%5Csim%5Cmathcal%7BD%7D%2Cy%7D%5Be%5E%7B-y%28H%28x%29&plus;%5Calpha%20h%28x%29%29%7D%5D)

The loss can be decomposed to each instance, which is called pointwise loss, as

![loss_{\exp}(H+\alpha h|x)=\mathbb{E}_y[e^{-y(H(x)+\alpha h(x))}|x]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20loss_%7B%5Cexp%7D%28H&plus;%5Calpha%20h%7Cx%29%3D%5Cmathbb%7BE%7D_y%5Be%5E%7B-y%28H%28x%29&plus;%5Calpha%20h%28x%29%29%7D%7Cx%5D)

Since y and h(x) must be +1 or -1, we can expand the expectation as

![loss_{\exp}(H+\alpha h|x)=e^{-yH(x)}\big(e^{-\alpha}P(y=h(x)|x)+e^{\alpha}P(y\neq h(x)|x)\big)](http://latex.codecogs.com/gif.latex?loss_%7B%5Cexp%7D%28H&plus;%5Calpha%20h%7Cx%29%3De%5E%7B-yH%28x%29%7D%5Cbig%28e%5E%7B-%5Calpha%7DP%28y%3Dh%28x%29%7Cx%29&plus;e%5E%7B%5Calpha%7DP%28y%5Cneq%20h%28x%29%7Cx%29%5Cbig%29)

Suppose we have already generated h, and thus the weight α that minimizes the
loss can be found when the derivative of the loss equals zero, that is,

![\begin{align*}\frac{\partial loss_{\exp}(H+\alpha h|x)}{\partial\alpha}&=e^{-yH(x)}\big(-e^{-\alpha}P(y=h(x)|x)+e^{\alpha}P(y\neq h(x)|x)\big)\\&=0\end{align*}](http://latex.codecogs.com/gif.latex?%5Cbegin%7Balign*%7D%5Cfrac%7B%5Cpartial%20loss_%7B%5Cexp%7D%28H&plus;%5Calpha%20h%7Cx%29%7D%7B%5Cpartial%5Calpha%7D%26%3De%5E%7B-yH%28x%29%7D%5Cbig%28-e%5E%7B-%5Calpha%7DP%28y%3Dh%28x%29%7Cx%29&plus;e%5E%7B%5Calpha%7DP%28y%5Cneq%20h%28x%29%7Cx%29%5Cbig%29%5C%5C%26%3D0%5Cend%7Balign*%7D)

and the solution is

![\alpha=\frac{1}{2}\ln\frac{P(y=h(x)|x)}{P(y\neq h(x)|x)}](http://latex.codecogs.com/gif.latex?%5Calpha%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cfrac%7BP%28y%3Dh%28x%29%7Cx%29%7D%7BP%28y%5Cneq%20h%28x%29%7Cx%29%7D)

By taking an expectation overx, that is, solving ![\frac{\partial loss_{\exp}(H+\alpha h)}{\alpha}=0](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cfrac%7B%5Cpartial%20loss_%7B%5Cexp%7D%28H&plus;%5Calpha%20h%29%7D%7B%5Calpha%7D%3D0), and denoting ![\epsilon=\mathbb{E}_{x\sim\mathcal{D}}[y\neq h(x)]](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cepsilon%3D%5Cmathbb%7BE%7D_%7Bx%5Csim%5Cmathcal%7BD%7D%7D%5By%5Cneq%20h%28x%29%5D), we get

![\alpha=\frac{1}{2}\ln\frac{\epsilon}{1-\epsilon}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Calpha%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cfrac%7B%5Cepsilon%7D%7B1-%5Cepsilon%7D)

which is the way of determining ![\alpha_t](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Calpha_t) in AdaBoost.

Now let’s consider how to generate h. We need to consider what hypothesis is desired for the next round, and then generate an instance distribution to achieve this hypothesis.

We can expand the pointwise loss to second order:

![\begin{align*}loss_{\exp}(H+h|x)&\approx\mathbb{E}_y[e^{-yH(x)}(1-yh(x)+y^2h(x)^2/2)|x]\\&=\mathbb{E}_y[e^{-yH(x)}-yh(x)+1/2)|x]\end{align*}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbegin%7Balign*%7Dloss_%7B%5Cexp%7D%28H&plus;h%7Cx%29%26%5Capprox%5Cmathbb%7BE%7D_y%5Be%5E%7B-yH%28x%29%7D%281-yh%28x%29&plus;y%5E2h%28x%29%5E2/2%29%7Cx%5D%5C%5C%26%3D%5Cmathbb%7BE%7D_y%5Be%5E%7B-yH%28x%29%7D-yh%28x%29&plus;1/2%29%7Cx%5D%5Cend%7Balign*%7D)

since ![y^2=1](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20y%5E2%3D1) and ![h(x)^2=1](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20h%28x%29%5E2%3D1).

Then a perfect hypothesis is

![\begin{align*}h^*(x)&=\arg\min_h loss_{\exp}(H+h|x)=\arg\max_h\mathbb{E}[e^{-yH(x)}yh(x)|x]\\&=\arg\max_h e^{-H(x)}P(y=1|x)\cdot 1\cdot h(x)+e^{H(x)}P(y=-1|x)\cdot(-1)\cdot h(x)\end{align*}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbegin%7Balign*%7Dh%5E*%28x%29%26%3D%5Carg%5Cmin_h%20loss_%7B%5Cexp%7D%28H&plus;h%7Cx%29%3D%5Carg%5Cmax_h%5Cmathbb%7BE%7D%5Be%5E%7B-yH%28x%29%7Dyh%28x%29%7Cx%5D%5C%5C%26%3D%5Carg%5Cmax_h%20e%5E%7B-H%28x%29%7DP%28y%3D1%7Cx%29%5Ccdot%201%5Ccdot%20h%28x%29&plus;e%5E%7BH%28x%29%7DP%28y%3D-1%7Cx%29%5Ccdot%28-1%29%5Ccdot%20h%28x%29%5Cend%7Balign*%7D)

Note that ![e^{-yH(x)}](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20e%5E%7B-yH%28x%29%7D) is a constant in terms of h(x). By normalizing the expectation as

![h^*(x)&=\arg\max_h \frac{e^{-H(x)}P(y=1|x)\cdot 1\cdot h(x)+e^{H(x)}P(y=-1|x)\cdot(-1)\cdot h(x)}{e^{-H(x)}P(y=1|x)+e^{H(x)}P(y=-1|x)}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20h%5E*%28x%29%26%3D%5Carg%5Cmax_h%20%5Cfrac%7Be%5E%7B-H%28x%29%7DP%28y%3D1%7Cx%29%5Ccdot%201%5Ccdot%20h%28x%29&plus;e%5E%7BH%28x%29%7DP%28y%3D-1%7Cx%29%5Ccdot%28-1%29%5Ccdot%20h%28x%29%7D%7Be%5E%7B-H%28x%29%7DP%28y%3D1%7Cx%29&plus;e%5E%7BH%28x%29%7DP%28y%3D-1%7Cx%29%7D)

we can rewrite the expectation using a new term ![w(x,y)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20w%28x%2Cy%29), which is drawn from ![e^{-yH(x)}P(y|x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29), as

![h^*(x)=\arg\max_h\mathbb{E}_{w(x,y)\sim e^{-yH(x)}P(y|x)}[yh(x)|x]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20h%5E*%28x%29%3D%5Carg%5Cmax_h%5Cmathbb%7BE%7D_%7Bw%28x%2Cy%29%5Csim%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29%7D%5Byh%28x%29%7Cx%5D)

Since ![h^*(x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20h%5E*%28x%29) must be +1 or -1, the solution to the optimization is that ![h^*(x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20h%5E*%28x%29) holds the same sign with y|x, that is,

![\begin{align*}h^*(x)&=\mathbb{E}_{w(x,y)\sim e^{-yH(x)}P(y|x)}\\&=P_{w(x,y)\sim e^{-yH(x)}P(y|x)}(y=1|x)-P_{w(x,y)\sim e^{-yH(x)}P(y|x)}(y=-1|x)\end{align*}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbegin%7Balign*%7Dh%5E*%28x%29%26%3D%5Cmathbb%7BE%7D_%7Bw%28x%2Cy%29%5Csim%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29%7D%5C%5C%26%3DP_%7Bw%28x%2Cy%29%5Csim%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29%7D%28y%3D1%7Cx%29-P_%7Bw%28x%2Cy%29%5Csim%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29%7D%28y%3D-1%7Cx%29%5Cend%7Balign*%7D)

As can be seen, ![h^*(x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20h%5E*%28x%29) simply performs the optimal classification of x under the distribution ![e^{-yH(x)}P(y|x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29). Therefore,![e^{-yH(x)}P(y|x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20e%5E%7B-yH%28x%29%7DP%28y%7Cx%29) is the desired distribution for a hypothesis minimizing 0/1-loss.

So, when the hypothesish(x) has been learned and ![\alpha=\frac{1}{2}\ln\frac{\epsilon}{1-\epsilon}](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Calpha%3D%5Cfrac%7B1%7D%7B2%7D%5Cln%5Cfrac%7B%5Cepsilon%7D%7B1-%5Cepsilon%7D) has been determined in the current round, the distribution for the next round should be

![\begin{align*}\mathcal{D}_{t+1}(x)&=e^{-y(H(x)+\alpha h(x))}P(y|x)\\&=e^{-yH(x)}P(y|x)\cdot e^{-\alpha yh(x)}\\&=\mathcal{D}_t(x)\cdot e^{-\alpha yh(x)}\end{align*}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbegin%7Balign*%7D%5Cmathcal%7BD%7D_%7Bt&plus;1%7D%28x%29%26%3De%5E%7B-y%28H%28x%29&plus;%5Calpha%20h%28x%29%29%7DP%28y%7Cx%29%5C%5C%26%3De%5E%7B-yH%28x%29%7DP%28y%7Cx%29%5Ccdot%20e%5E%7B-%5Calpha%20yh%28x%29%7D%5C%5C%26%3D%5Cmathcal%7BD%7D_t%28x%29%5Ccdot%20e%5E%7B-%5Calpha%20yh%28x%29%7D%5Cend%7Balign*%7D)

which is the way of updating instance distribution in AdaBoost.

But, why optimizing the exponential loss works for minimizing the 0/1-loss? 

Actually, we can see that

![h^*(x)=\arg\min_h\mathbb{E}_{x\sim\mathcal{D},y}[e^{-yh(x)}|x]=\frac{1}{2}ln\frac{P(y=1|x)}{P(y=-1|x)}](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20h%5E*%28x%29%3D%5Carg%5Cmin_h%5Cmathbb%7BE%7D_%7Bx%5Csim%5Cmathcal%7BD%7D%2Cy%7D%5Be%5E%7B-yh%28x%29%7D%7Cx%5D%3D%5Cfrac%7B1%7D%7B2%7Dln%5Cfrac%7BP%28y%3D1%7Cx%29%7D%7BP%28y%3D-1%7Cx%29%7D)

and therefore we have

![sign(h^*(x))=\arg\max_y P(y|x)](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20sign%28h%5E*%28x%29%29%3D%5Carg%5Cmax_y%20P%28y%7Cx%29)

which implies that the optimal solution to the exponential loss achieves the minimum Bayesian error for the classification problem.

Moreover, we can see that the function ![h^*(x)](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20h%5E*%28x%29) which minimizes the exponential loss is the logistic regression model up to a factor 2. So, by ignoring the factor 1/2, AdaBoost can also be viewed as fitting an additive logistic regression model.

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

2 Get back a hypothesis ![h_t:X\times Y\rightarrow[0,1]](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t%3AX%5Ctimes%20Y%5Crightarrow%5B0%2C1%5D)

3 Calculate the pseudo-loss of ![h_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_t): ![\epsilon_t=\frac{1}{2}\sum_{(i,y)\in B}D_t(i,y)(1-h_t(x_i,y_i)+h_t(x_i,y))](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cepsilon_t%3D%5Cfrac%7B1%7D%7B2%7D%5Csum_%7B%28i%2Cy%29%5Cin%20B%7DD_t%28i%2Cy%29%281-h_t%28x_i%2Cy_i%29&plus;h_t%28x_i%2Cy%29%29).

4 Set ![\beta_t=\epsilon_t/(1-\epsilon_t)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Cbeta_t%3D%5Cepsilon_t/%281-%5Cepsilon_t%29).

5 Update distribution ![D_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_t): ![D_{t+!}(i,y)=\frac{D_t(i,y)}{Z_t}\cdot\beta^{(1/2)(1+h_t(x_i,y_i)-h_t(x_i,y))}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;%21%7D%28i%2Cy%29%3D%5Cfrac%7BD_t%28i%2Cy%29%7D%7BZ_t%7D%5Ccdot%5Cbeta%5E%7B%281/2%29%281&plus;h_t%28x_i%2Cy_i%29-h_t%28x_i%2Cy%29%29%7D)

where ![Z_t](http://latex.codecogs.com/gif.latex?%5Cbg_white%20Z_t) is a normalization constant (chosen so that ![D_{t+1}](http://latex.codecogs.com/gif.latex?%5Cbg_white%20D_%7Bt&plus;1%7D) will be a distribution).

**Output** the hypothesis: ![h_{fin}(x)=\arg\max_{y\in Y}\sum_{t=1}^{T}\left(\log\frac{1}{\beta_t}\right)h_t(x,y)](http://latex.codecogs.com/gif.latex?%5Cbg_white%20h_%7Bfin%7D%28x%29%3D%5Carg%5Cmax_%7By%5Cin%20Y%7D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Cleft%28%5Clog%5Cfrac%7B1%7D%7B%5Cbeta_t%7D%5Cright%29h_t%28x%2Cy%29).

### Real AdaBoost

> Freidman, Hastie, Tibshirani. Additive Logistic Regression: A Statistical View of Boosting

1 Start with weights ![w_i=1/N](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20w_i%3D1/N), ![i=1,2,\dots,N](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20i%3D1%2C2%2C%5Cdots%2CN).

2 Repeat for ![m=1,2,\dots,M](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20m%3D1%2C2%2C%5Cdots%2CM):

(a) Fit the classifier to obtain a class probability estimate ![p_m(x)=\hat{P}_w(y=1|x)\in[0,1]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20p_m%28x%29%3D%5Chat%7BP%7D_w%28y%3D1%7Cx%29%5Cin%5B0%2C1%5D), using the weights ![w_i](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20w_i) on the training data.

(b) Set ![f_m(x)\leftarrow\frac{1}{2}\log\frac{p_m(x)}{1-p_m(x)}\in R](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20f_m%28x%29%5Cleftarrow%5Cfrac%7B1%7D%7B2%7D%5Clog%5Cfrac%7Bp_m%28x%29%7D%7B1-p_m%28x%29%7D%5Cin%20R).

(c) Set ![w_i\leftarrow w_i\exp[-y_if_m(x_i)]](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20w_i%5Cleftarrow%20w_i%5Cexp%5B-y_if_m%28x_i%29%5D), ![i=1,2,\dots,N](http://latex.codecogs.com/gif.latex?%5Cdpi%7B100%7D%20%5Cbg_white%20i%3D1%2C2%2C%5Cdots%2CN), and renormalize so that ![\sum_i w_i=1](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cbg_white%20%5Csum_i%20w_i%3D1).

3 Output the classifier ![\sign[\sum_{m=1}^{M}f_m(x)]](http://latex.codecogs.com/gif.latex?%5Cinline%20%5Cbg_white%20%5Csign%5B%5Csum_%7Bm%3D1%7D%5E%7BM%7Df_m%28x%29%5D)
