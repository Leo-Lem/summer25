[exercises](exercises.pdf) | [slides](slides.pdf)
# Basic Math
**Closed-form solution**: inputs yield correct outputs directly.
- explicit formula.
- no iteration.
- deterministic computation.
**iid-assumption**: identically and independently distributed.
**Gaussian/\[standard\] normal distribution**: bell curve with mean $\mu[=0]$ and variance $\sigma^2[=1]$.
**Bayes' Law**: $p(A|B)=p(B|A)\frac{p(A)}{p(B)}$.
## Linear Algebra
**Rank** $rank(A)=$ linearly independent columns. dimension of spanned vector space.
**Norms**: lengths/size of vector. non-negative, homogenous, triangle unequal.
- 0-"norm": non-zero entries. not actually a norm.
- 1-norm: sum.
- 2 (Euclid): root of squares.
- $\infty$ (max): maximum value.
- $p$-norm $||x||_p=(\sum_i{|x_i|^p})^{1/p}$. other norms derive from this. also called Lebesgue norm $\ell_p$.
**Determinant** $det(A)=ad-bc$. factor of area increase or decrease.
- 3x3: diagonals - reverse diagonals.
**Trace** $tr(A)=a+c$. sum of main diagonal.
**Inverse** $AA^{-1}=I$. Reverse of transformation (only exists if $det(A)\neq0$).
**Eigenvector & -value** $A\overset{\rightarrow}{v}=\lambda\overset{\rightarrow}{v}$. 
- Eigenvalue $\lambda$: solve $\det{(A-\lambda I)}=0$.
- Eigenvector $v$: only scaled in transformation (by Eigenvalue). Plug $\lambda$s into $(A-\lambda I)v=0$.
**Definiteness**: nature (convexity, concavity) of matrix-related quadratic form $x^\top Ax$.
- positive definite PD for $\lambda>0$.
- positive semidefinite PSD for $\lambda≥0$.
- analog for ND, NSD.
- indefinite means neither convex nor concave.
## Operations
**Gaussian elimination**: lower triangle. eliminate variables.
**Matrix multiplication**: row x column.
**Inner product**: linear (in one argument), symmetric, non-negative (psd), strictly definite iff 0 only for 0 vector. dot product is example.
**Matrix factorisation**: TODO
## Optimisation
**gradient**: partial derivates.
**convex sets**: all points are connected with other points.
**convex functions**: convex set and connection is contained in shape. compute second derivative and check if > 0.
- linear: convex and concave.
- p-norm: convex (but not 0-norm).
- square: convex for $A\succeq0$ ($w^TAw$).
- absolute: non-strictly convex.
**exact line search for step length/learning rate**: if i move only along given line, how far should i move to minimise?
# Concepts
**Empirical risk minimisation** ERM: minimise average loss over training data.
**$k$-fold cross validation**.
- split data into blocks.
- use each block for validation once, others for training.
- train $k$ times.
**Bias v. variance**
- high variance $E[(f_n(x)-E[f_n(x)])^2]$ $\to$ high complexity, capture training data well, but overfit.
- high bias $E[f_n(x)]-f^*(x)$ $\to$ low complexity, might generalise better, but underfit.
## Maximum Likelihood Principle
_Maximise the likelihood of the observation assuming the model is correct._
**Maximum Likelihood Estimator**: $\max_\theta p(\text{observation}|\theta)$.
- Gauss yields mean (sum of squared differences minimised by mean).
- Laplace yields median (sum of absolute differences minimised by median).
- MLE is specific ERM with negative log-likelihood loss.
**Maximum A Posteriori** MAP: $\max_\theta p(\theta|\text{observation})=p(\text{observation})\frac{p(\theta)}{p(\text{observation})}$.
- MAP is specific RRM where regularisation is log-prior.
- use over MLE, when you want to incorporate prior knowledge.
## Model comparison
_Compare two models using significance test._
**Input**: two models and evaluation metric.
$H_0$: both models perform equally well.
**Likelihood of $H_0$** denoted by $p$.
Permutation test to approximate $p$. target usually lower than .05 or .01 $\to$ can reject $H_0$.
## Discriminative v. Generative
Discriminative models find decision boundary: $p(y|x)$.
Generative models find distribution: $p(x,y)$. can be used to generate new data points.
Gaussian MLE (assume Gaussian distribution)
- Linear Discriminant Analysis (LDA): shared covariance matrix.
- Quadratic Discriminant Analysis (QDA): different covariance matrix per class.
## Dimensionality Reduction, Embeddings
### Principal Component Analysis
_Technique to reduce the dimension of a dataset in $\mathbb{R}^d$ by linear projections._
**Covariance matrix approach**: maximise variance of reduced (projected) data.
- assume the points are centred, otherwise center with $\tilde{x}_i=x_i-\bar{x}$.
- project data on the space spanned by the eigenvectors of the $l$ largest eigenvalues of the covariance matrix $X^\top X$.
- eigenvectors are called principal components (or axes/directions).
- reconstruction or projection error: distance between point and projection.
**SVD approach**: minimise squared error. leads to same solution.
**Outliers**: optimise global criteria, no guaranty for individual points, sensitive to outliers.
**Use case**: works best for Gaussian.
**Applications**: dimensionality reduction, data visualisation, noise filtering, feature extraction.
**Kernel PCA**: use kernel trick for non-linear principal components.
### Multi-dimensional scaling
_Transform set of objects by pairwise distances into points in geometric space while keepng relative distances._
Euclidian distance matrix $D$ comes from $\mathbb{R}^d$.
Match best by pairwise distances $\to$ many possibilities/variants.
1. Classic MDS: minimise error wrt pairwise scalar products. efficient computation of optimal solution.
2. Metric MDS: minimise error wrt distance matrix D. highly non-convex, NP-hard problem.
3. Non-metric MDS: only ordering on distances is tried to preserve.
**Manifold**: locally euclidian, globally curved or complex (earth's surface, for example).
**Isometric mapping** (isomap)
- compute geodesic distance (distance on the manifold): construct kNN graph to approximate.
- compute shortest path distances between all pairwise data points.
- store distance matrix D.
- run metric DMS on D.
# Regression
## (Ordinary) Least Squares
_Find best-fitting linear function $\min_{\tilde{w}}{{\frac{1}{2}||\tilde{X}\tilde{w}-y||}^2}$. not eliminating loss -> always a solution._
**Weights**: influence of each parameter on result.
**Offset**: general bias. can be integrated into as weight 0: $\tilde{x}$ column 0.
**Gradient**: $\nabla L=X^{\top}(Xw-y)$. Solve for 0: $(X^\top X)w=X^\top y$.
**Runtime**: $O(d^3)$.
## Evaluation
_How good is our regression?_
**Mean squared error** $MSE=\frac1n\sum_{i=1}^n{(y_i-\hat{y}_i)^2}$. Penalise larger errors more than small ones. less interpretable due to square.
**Root mean squared error** $RMSE=\sqrt{MSE}$. improves interpretability over MSE.
**Mean absolute error** $MAE=\frac1n\sum_{i=1}^n{|y_i-\hat{y}_i|}$. more robust/less sensitive to individual errors.
**Coefficient of Determination** $R^2=1-\frac{\sum{(y_i-\hat{y}_i)^2}}{\sum{(y_i-\bar{y})^2}}$. 1 means perfect prediction, 0 means same as predicting the mean, negative means worse performance that constant predictor.
## Polynomial regression and basis functions
_Map to higher-dimension linear regression._
**Mapping** $x \to \tilde{x}=(x^d,x^{d-1},…,x,1)^\top\in \mathbb{R}^{d+1}$.
**works for arbitrary function**: we can model anything theoretically.
**problem**: over- and underfitting.
## Adding regularisation
_Prevent overfitting by penalising complexity/encouraging simpler models._
**L1-regularisation** $\min_w{L(w)+\lambda||w||_1}$. Sharp corners $\to$ Encourages sparsity.
- LASSO regression when used with least squares.
- Useful when few features contribute (weights can be zero-ed).
**L2-regularisation** $\min_w{L(w)+\frac{\lambda}{2}||w||_2^2}$. Encourages shrinkage.
- Ridge regression when used with least squares. 0-gradient $X^\top X+n\lambda I=X^\top y$.
- Useful when many features contribute a little bit (weights are usually not zero-ed)
**Elastic Net**: interpolation between ridge and lasso.
**More regularisations**: dropout (in NNs), varied input, early stopping.
**Finding** $\lambda$.
1. solve for many $\lambda$.
2. regularisation paths: $k$-fold cross validation for each.
3. minimal validation error: pick best $\lambda^*$.
4. train with $\lambda^*$.
**Feature scaling required for regularisation**.
- scale to [0,1] or [-1,1].
- normalising: center, then scale such that 2-norm is one.
## Handling outliers
_OLS is very sensitive to outliers due to squared residuals._
**Least absolute deviations** LAD $min_w\frac{1}{n}||Xw-y||_1$. absolute residuals instead of squared residuals.
- also called L1 or median regression.
- often with different regulariser than L1.
# Classification
## Binary Classification
*Predict yes or no, -1 or +1 $\to$ separate points by hyperplane (n-1 dimensional plane).*
**Intuitive loss function**: $l(y,\hat{y})=\begin{cases}0 & \text{if } y = \hat{y} \\ 1 & \text{if } y \neq \hat{y} \end{cases}$. NP-hard because of the jump in the loss function.  
  $\to$ not differentiable and thus no gradient.
## Logistic regression
*Use log loss instead $f(x)=\log{(1+\exp{(-y\cdot (x^\top w+b)}))}$.*
- **Misleading name**: No regression but actually classification.
- **Logistic function**: smooth approximation of the step function. $p(y=1|x)=\frac{1}{1+\exp{(-(x^\top w+b))}}$.
- **MLE**: Logistic regression is the MLE when using logistic function.
**More loss functions**: Hinge $max(0,1-t)$. Squared hinge $max(0,1-t)^2$.
## Support Vector Machines
*wiggle the hyperplane for more robust classifier $\to$ maximize margin between + and - points.*
- hard v. soft margin: no points inside margin v. allow small error.
- constrained convex optimization problem $\to$ can be solved efficiently.
- 2-norm regularizer and hinge loss leads to SVM.
- $\xi_i$: slack variable which allows margin of error.
- $C$ balances large margin and violation terms: error budget.
- dual: $w^*=\sum^n \alpha_i^*y_ix_i$ with dual solution $\alpha^*$. only when $\alpha_i>0$ the data point is impactful $\to$  support vector.
	- $\alpha_i^*=0$: data point is outside the margin and correctly classified.
	- $0<\alpha_ i^*<C$: data point is on correct margin.
	- $\alpha_i^*=C$: data point is inside margin or on wrong side.
**Non-linear SVM and kernels**: kernels are a shortcut for basis function trick (which is infeasible due to high number of basis functions)
- kernel: implicit mapping of data to higher-dimensional space without need to compute embedding/feature map explicitly (kernel trick).
- Inner product/dot product $K(x,y)=\langle \Phi(x), \Phi(y) \rangle=\sum_{k=0}^{s}{\Phi(x)\cdot\Phi(y)}$.
- prove kernel function: $K(=k(x_i,x_j))\succeq 0$. If $K$ is psd then map $\Phi$ exists.
- scaling and adding psd matrices still stays psd.
- kernel function measures how similar two datapoints are in feature space.
- linear $k=x_i^\top x_j$.
- cosine similarity $k=\frac{x_i^\top x_j}{||x_i||\cdot ||x_j||}$.
- Gaussian (or radial basis function RBF) $k=\exp(\frac{-||x_i-x_j||_2^2}{2\sigma^2})$.
- Polynomial $k=(x_i^\top x_j+c)^s$.
**Smoothmax**: lets logistic regression act like soft-margin SVM. Logistic regression is probabilistic, smooth-margin classifier, SVM impose strict geometric constraints.
**Linear $\to$ non-linear**: any linear can be transformed into non-linear with basis functions or kernels (2-norm regularizer).
**Parametric v. non-parametric**: fixed number of parameter or not fixed a priori (depends on data points, is infinite, …).
**Multiclass classification**
- one-versus-rest (OvR): train for each class treating only that class as positive.
- one-versus-one (OvO): train for each pair of classes.
- direct methods: multinomial logistic regression, k-NN, …
## k-Nearest Neighbor
*similar datapoints should have similar labels. good first choice.*
**algorithm**: find k nearest neighbors for point, (weighted/unweighted) majority vote of neighbor labels determines label, distance can use different measures.
**choice of $k$**: small k can lead to overfitting, large to underfitting. optimal value depends. good value can be found using cross-validation.
**advantages**: simple/easily understandable, no training, non-parametric (can handle complex decision boundaries), good at multiclass.
**disadvantages**: computationally expensive for large datasets, sensitive to irrelevant features and noisy data.
can also be used for regression.
**higher-dimensions hurt knn**: distances become less meaningful as all points become more or less the same distance apart $\to$ curse of dimensionality.
## Naive Bayes
*probabilistic algorithm based on Bayes' theorem.*
**Naive assumption**: all features are conditionally independent given the class.
**Bayes' theorem**: $p(A|B)=p(B|A)\frac{p(A)}{p(B)}$.
**For many classes**: $p(y|x_1,x_2,,x_n)=P(y)\frac{P(x_1,x_2,,x_n|y)}{P(x_1,x_2,,x_n)}=P(y)\prod{P(x_i|y)}$. joint likelihood is product of individual likelihoods.
**Laplacian smoothing**: to prevent 0 probabilities (add $\lambda$ to the frequency of each $x_i$).
**Simple estimation**: $P(x_i|y)=\frac{\text{count}(x_i)+\lambda}{\text{count}(y)}$.
**Different estimations of $p(x_i|y)$ lead to variants**: Bernoulli NB (for binary), Multinomial NB, Gaussian NB, Binomial NB, …
## Decision Trees
*Decision rules in tree structures, used for classification and regression.*
**Mental model**: Partitioning input space into output values.
**Recursive construction**
- Determine best split at each node: classification error, GINI index, entropy, …
- Check each dimension's (x, y, for example) best split and see which produces least error.
**Properties**
- NP-hard to determine optimal DT.
- independent of feature scaling.
- sensitive to small changes in data and rotation.
- Prone to overfitting with small dataset.
**Regression**: nodes represent constant functions, otherwise same approach as for classification.
**Many algorithms**: ID3, C4.5, CART, …
## Evaluation
**Accuracy** $ACC=\frac{\text{number of correct predictions}}{\text{total number of predictions}}$. simple and intuitive, misleading for imbalanced classes.
**Confusion matrix** (Contingency table): Actual against predicted counts (yields true/false positives/negatives).
**Precision** $P=\frac{TP}{TP+FP}$. proportion of predicted positives that are true.
**Recall** $R=\frac{TP}{TP+FN}$. proportion of actual positives that are predicted correctly.
**F1 score** $F1=2\frac{P\cdot R}{P+R}$. harmonic mean of precision and recall.
### Multi-class Averaging
**Macro**: $\text{Macro}=\frac1K\sum_{k=1}^K{\text{Metric}_k}$. independent computation, average equally. treat all classes the same. useful when classes are equally important.
**Micro**: $Micro=\text{Metric}_{\sum_k}$. aggregate TP/FP/FN, compute metric on totals. favour frequent classes. useful when overall performance is most important.
## Prior knowledge
**Feature engineering**: e.g., combine age+BMI into metabolic risk feature based on clinical knowledge.
**Synthetic data**: e.g., if certain symptoms indicate disease, create examples of that in data.
Encode knowledge in model: monotonic constraints in gradient boosting (price increases with size, for example).
**Bayesian priors**: in Naive Bayes base prior class probabilities on distributions.
**Regularisation with priors**: L1/L2 regularisation encodes prior knowledge that features are sparse.
**Rule-based/hybrid models**: first apply linguistic rule, then classifier (in NLP).
## Loss functions
L1 loss: absolute deviation $\hat{y}-y$
L2 loss: squared deviation $(\hat{y}-y)^2$
Hinge loss (for labels $-1:1$): $\max{(0, 1-\hat{y}\cdot y)}$.
Logistic loss (for labels $0:1$): $\log{(1+\exp{(-y\cdot (x^\top w+b)}))}$.
# Learning
## Ensemble Learning
*Use different models and combine their results.*
**Bootstrapping**: use multiple subsamples to create bootstrap estimators to get an indication of the estimator's distribution.
**+Bagging**: aggregate the bootstrap estimators.
**Random Forest**: construct individual DTs with bootstrap subsamples.
- Predict: obtain all predictions and majority vote (classification) or average (regression).
- Parameters (generally not too important, as RF are relatively stable)
	- number $m$ of subsamples (for sampling with replacement $m=n$).
	- number $p$ of dimensions (usually $d/3$).
	- $n_{min}=1$ so the tree becomes deep (leads to individual overfitting, but reduce by bagging).
## Unsupervised Learning
*Find structure in unlabelled dataset.*
**Approaches**: clustering, dimensionality reduction, anomaly detection, density estimation.
### k- means
*group data into k clusters with centres $\mu_i$. Non-convex optimisation.*
**Lloyd's algorithm**
1. start with random centres.
2. assign all points to closest center.
3. define new centres as mean vectors of current clusters. back to 2.
**Termination**: finite number of iterations or end at local minimum (arbitrarily bad solution possible).
**Refined initialisation**: use simpler clustering algorithm for initial means.
**In practice**: run often with different parameters and pick best.
k-means leads to Voronoi partition.
Many variants exist.
## Deep Learning

