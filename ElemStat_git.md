The Elements of Statistical Learning
================

Ch1
---

6/16/2017

1.  Supervised learning: having the presence of outcome variable to guide the learning process. Unsupervised learning:have no measurement of the outcome, our task is clustering.

2.  Classification problem(predict categorical output)and regression problem(predict quantitative output)are Supervised learning;while clustering is Unsupervised learning.

Ch2
---

6/18/2017

1.  Linear model makes huge assumption, yield stable but probably inaccurate predictions(low variance and high bias); while K-nearest neighbors model make mild assumptions, its predictions often accurate but unstable

<span style="color:red"> 2. P12, 1st paragraph, what is affine set? 2nd paragraph, why steepest uphill direction? </span>

1.  The error on the training dataset should be approximately an increasing function of k for k-nearest neighbor fit; cannot use sum of squared error as a criteria for picking k.

2.  The effective number of parameters in k-nearest neighbor is N/k, i.e., if non-overlapping, we need fit N/k means for totally N/k neighborhoods

3.  If the training data is simulated from independent Gaussian distributions, least square is appropriate for prediction; if from mixture Gaussian, k-nearest neighbor is better.

6/19/2017

1.  Bullets on P17,P18: kernel methods, local regression ... enhanced the simple 1(k)-nearest neighbor procedure. Kernel methods having weights decrease smoothly to zero with distance from the target point, rather than the 0/1 weights used by k-nearest neighbors.

2.  Minimize the squared prediction error(EPE) loss, *E**P**E*(*f*)=*E*<sub>*x*</sub>*E*<sub>*Y*|*X*</sub>(\[*Y* − *f*(*X*)\]<sup>2</sup>|*X*), get solution *f*(*x*)=*E*(*Y*|*X* = *x*), i.e., the conditional expectation(known as the regression function). Nearest-neighbor approximates $\\hat{f}(x)=Ave(y\_i|x\_i \\in N\_k(x))$. Under mild condition on P(X,Y), as N,k →∞ such that k/N → 0, $\\hat{f}(x) \\rightarrow E(Y|X=x)$. The convergence still holds but the rate of convergence decreases as the dimension p increases.

3.  Additive model solves the high dimensional problem by approximating the universal conditional expectation simutaneously for each of the coordinate function *f*<sub>*j*</sub> in $f(X)=\\sum\_{j=1}^pf\_j(X)$.

4.  If *L*<sub>1</sub> loss: *E*|*Y* − *f*(*X*)|, the solution will be conditional median *f*(*x*)=*m**e**d**i**a**n*(*Y*|*X* = *x*). The discontinuity in its derivatives hendered their wide use.

5.  Loss function for categorical prediction is represented by a matrix L=card(G) with 0 on the diagonal and nonnegative elsewhere(often 1s). <span style="color:red"> How to calculate (2.19) ~ (2.23)? </span>

6/20/2017

1.  Curse of dimensionality: (1) To capture a fraction r of a p-dimensional hypercube, the expected edge length will be *r*<sup>1/*p*</sup>, i.e., to capture 1% of the data forming a local hypercube, we need to vover 63% of the range in each dimension/variable of the input;

(2)Mean distance of the closest point increases for a large *p* so the prediction is more difficult near the edges of the training sample;

(3)Sampling density is proportional to *N*<sup>1/*p*</sup>, i.e., 100<sup>10</sup> sample needed for p=10 to get same sample density of 100 in 1D.

(4)The complexity of function(Y=f(X)) with many variables(larger p) can grow with the dimension p, and if we want to estimate such functions with same accuracy as in low dim, then we need the size of training data grow exponentially.

2.Calculation in (2.27) shows why prediction error have additional variance *σ*<sup>2</sup>.

1.  If we assume it's a linear model, (2.28) shows the expected EPE increase linearly in p. By imposing linear restrictions, we have avoided the curse of dimensionality.

6/21/2017

1.  <span style="color:red"> how to get the $\\hat{y}\_0$ on the bottom of page 24? </span>

2.  figure 2.9 shows comparison of least square and 1-nearest neighbor with their ration for two senario(get the way of comparison). There is acutally a whole spectrum of methods between the rigid linear models and the extreme flexible 1-nearest neighbor models. Section 2.6 using other f(X), specifically designed to overcome the dimensionality problem.

3.  In additive error model,*Y* = *f*(*X*)+*ϵ*,*ϵ* is independent of X.More often, (X,Y) will not have a deterministic relationship *Y* = *f*(*X*), so the additive model assume that we can capture all the departures from a deterministic relationship via the error *ϵ*.

4.  <span style="color:red"> In the beginning of 2.6.1, Why the conditional distribution *P*(*Y*|*X*) depends on *X* only through the conditional mean *f*(*x*)=*E*(*Y*|*X* = *x*)? </span>

5.Two ways of understanding: Supervised learning VS function approximation. Learning by example: the learning algorithm modify its input/output relationship in response to the prediction error; In terms of function approximation, we imagine our parametrized function as a surface in p+1 dim space and we observed noisy representations from it.

1.  The principle of MLE assumes that the most reasonable values for *θ* are those for which the probability of the observed sample is largest.
