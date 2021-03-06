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

4.  <span style="color:red"> In the beginning of 2.6.1, Why the conditional distribution *P*(*Y*|*X*) depends on *X* only through the conditional mean *f*(*x*)=*E*(*Y*|*X* = *x*)? Answered in equation (2.34). </span>

5.  Two ways of understanding: Supervised learning VS function approximation. Learning by example: the learning algorithm modify its input/output relationship in response to the prediction error; In terms of function approximation, we imagine our parametrized function as a surface in p+1 dim space and we observed noisy representations from it.

6.  The principle of MLE assumes that the most reasonable values for *θ* are those for which the probability of the observed sample is largest.

6/22/2017(Ch2 P32-P34)

1.  need Approaches to make efficient use of structured data. There are infinitely many solutions for $\\hat{f}$, so we impose restritions on eligible solutions.

2.  Most training methods imposed complexity restrictions in small neighborhood of input space, e.g., $\\hat{f}$ exhibits special structure such as nearly constant, linear or low order polynomial behavior in the small neighborhood.

3.  Any method that attempt to produce locally varying functions in small isotropic neighborhood will run into problems in high dimension; all methods that overcome the dimensionality problems have an associated metric for measuring neighborhoods, which does not allow the neighborhood to be simutaneously small in all directions.

4.  nonparametric methods falls in several classes and each of the classes has associated with one or more smoothing parameters that control the effective size of the local neighborhood.

5.  <span style="color:red"> why called adaptively chosen basis function methods in the last and second last paragraph of page 36? </span>

6/23/2017(Ch2 P34-P38)

1.  Roughness penalty controls the second derivative of *f*, to get a smooth solution. Penalized least-sqaure criterion
    $$PRSS(f;\\lambda)= \\sum\_{i=1}^N(y\_i -f(x\_i))^2 + \\lambda\\int\[f''(x)\]^2dx$$
    . when *λ* = ∞, only linear function(the most smooth) are permitted.

2.  Penalty function, or regularization methods express our prior belief that the type of functions we seek exhibit smooth behavior.

3.  Kernal methods specified the nature of the local neighborhood. Kernal function *K*<sub>*λ*</sub>(*x*<sub>0</sub>, *x*) assigns weights to points x in a region around *x*<sub>0</sub>. Define a local regression estimate $f\_{\\hat{\\theta}}(x\_0)$ where $\\hat{\\theta}$ minimizes
    $$RSS(f\_{\\theta},x\_0)=\\sum\_{i=1}^NK\_{\\lambda}(x\_0,x\_i)(y-f\_{\\theta}(x\_i))^2$$

4.  Basis functions: the model *f* is a linear expansion of basis functions
    $$f\_{\\theta}(x)=\\sum\_{m=1}^M\\theta\_mh\_m(x)$$
     The term linear refers to the action of parameter *θ*.

5.  <span style="color:red"> Didn't understand the 2nd paragraph on Page36, reread it after reading Ch5. Spline basis has knots. In general, we would like the data to dictate them as well but that will lead to a hard nonlinear problem. </span>

6.  All the above models have a smoothing or complexity parameter: The multiplier of the penalty term; the width of the kernel; the number of basis functions. We cannot use residual sum-of-squares on the training data to determine these parameters since it will always pick the interpolation fits hence zero residuals.

7.  As the model complexity increases, the variance tends to be increase and bias decreases. k-nearest neighbor as k increase, variance decrease and squared bias increases.

8.  Figure 2.11 shows the typical behavior of test error and training error: as model complexity increase, the training error would decrease since the model adapts itself too closely to the training data(overfitting) and will not generalize well(large test error).

6/24/2017(Ch3 P43-P46,Notes made up on 6/25)

1.  Linear model assumes that the regression function *E*(*Y*|*X*) is linear <span style="color:red"> in X not in *β*! </span>. Linear models can be applied to transformations(like the basis) of the input, which considerably expand their scope.

2.  Even if the *x*<sub>*i*</sub> were not drawn randomly, the least square criterion is still valid if the *y*<sub>*i*</sub>'s are conditionally independent given the input *x*<sub>*i*</sub>.<span style="color:red"> (Did not assume normality in LSE, right?)</span>

3.  The estimate $\\hat{y}$ is the orthogonal projection of y onto the subspace spanned by x, and residual vector $y-\\hat{y}$ is orthogonal to this subspace.

4.  If X is not full rank,*X*<sup>*T*</sup>*X* is singular and the least square coefficients $\\hat{\\beta}$ are not uniquely defined. However, the fitted values $\\hat{y}$ are still the projection of y onto the column space of X; there is just more than one way to express that projection in terms of X.

5.  Rank deficiency can also occur in signal and image analysis, where *p* &gt; *N*. In this case, the features are typically reduced by filtering or controlled by regularization.

6/25/2016 (Ch3 P46-)

1.
$$Var(\\hat{\\beta})=(X^TX)^{-1}\\sigma^2$$
 To draw inference about the parameters and the model, need additional Gaussian assumption
$$\\hat{\\beta} \\sim N(\\beta,(X^TX)^{-1}\\sigma^2 )$$
$$(N-p-1)\\hat(\\sigma^2) \\sim \\sigma^2\\chi^2\_{N-p-1}$$
 $\\hat{\\beta}$ and $\\hat{\\sigma}^2$ are statistically independent.
