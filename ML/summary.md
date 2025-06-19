[exercises](exercises.pdf) | [slides](slides.pdf)
# Linear Algebra Basics
**Norms**
- 0-norm: non-zeros
- 1-norm: sum
- 2-norm (Euclid): root of squares
- $\infty$-norm (max): maximum
**Determinant**: factor of area increase or decrease. $det(A)=ad-bc$. 3x3: diagonals - reverse diagonals.
**Trace**: sum of main diagonal. $tr(A)=a+c$.
**Inverse**: reverse of a transformation. $AA^{-1}=I$. No inverse if $det(A)=0$.
**Eigenvector & -value**: vectors only scaled by Eigenvalue in transformation. $A\overset{\rightarrow}{v}=\lambda\overset{\rightarrow}{v}$. $(A-\lambda I)\overset{\rightarrow}{v}=\overset{\rightarrow}{0}$. Find $\lambda$ to make determinant zero. $\det{(A-\lambda I)}=0$.
**Definiteness**: PD ($\lambda>0$), PSD ($\lambda≥0$), anlg. for negative
**Rank**: output dimensions. linearly independent columns.
**Gaussian elimination**: lower triangle. eliminate variables.
**Matrix multiplication**: row x column.
# Concepts
## Optimisation
**gradient**: partial derivates.
**convex sets**: all points are connected with other points.
**convex functions**: convex set and connection is contained in shape. compute second derivative and check if > 0.
**convexity rules**: linear is convex and concave. norm is convex. square is convex if $A$ is psd ($w^TAw$).
**exact line search for step length/learning rate**: if i move only along given line, how far should i move to minimise?
## Over-/Underfitting
**$k$-fold cross validation**: split data into blocks, use each block for validation once and others for training (train $k$ times).
**regularisation**: constrain magnitude/norm of model parameters. $\min_w{L(w)+\frac{\lambda}{2}||w||_2^2}$.
**approach**: solve for many $\lambda$, k-fold cross validation for each (called regularisation paths), pick best $\lambda^*$ (minimal validation error), train with $\lambda^*$.
Empirical risk minimisation ERM: minimise average loss over training data.
**Empirical (ERM) v. regularised risk minimisation (RRM)**: without and with regularisation.
**Bias v. variance**: high variance ($E[(f_n(x)-E[f_n(x)])^2]$) models have high model complexity and tend to overfit, but capture training data well. high bias ($E[f_n(x)]-f^*(x)$) models might underfit, but have small model complexity.
**Feature scaling**: some methods are invariant to feature scaling, regularisation is not. so always scale to [0,1] or [-1,1]. normalising: center, then scale such that 2-norm is one.
## Maximum Likelihood Principle
**Gaussian/normal distribution**: bell curve, defined by mean $\mu[=0]$ and variance $\sigma^2[=1]$ (bracket values are standard normal distribution).
**Closed-form solution**: explicit formula, no iteration, deterministic computation (inputs yield correct outputs directly).
**Assumption**: **i**dentically & **i**ndependently **d**istributed.
***M*aximum *L*ikelihood *E*stimator**: $\max_\theta p(\text{observation}|\theta)$.
- computation: With iid: $L(\theta)=\prod_{i=1}^n{p(t^i|\theta)}$. Plug in probability distribution (standard normal here) $L(\theta)=\prod_{i=1}^n{[\frac{1}{\sqrt{2\pi}}e^{-\frac{(t^i-\theta)^2}{2}}]}$. $\theta$ corresponds to the true value here and we are centering around this value (to estimate the likelihood). Simplify product to sum using $\log{L(\theta)}=:l(\theta)$. Derive for $\theta$, set equal to zero, solve for $\theta$.
- Gauss yields mean (sum of squared differences minimized by mean). Laplace yields median (sum of absolute differences minimized by median).
- Laplace is more robust against outliers (deviations grow linearly not squaredly).
- MLE is ERM with negative log-likelihood loss.
***M*aximum *A* *P*osteriori**: $\max_\theta p(\theta|\text{observation})=p(\text{observation})\frac{p(\theta)}{p(\text{observation})}$.
**Bayes Law**: $p(A|B)=p(B|A)\frac{p(A)}{p(B)}$.
**Risk minimisation equivalence**: MLE = ERM. MAP = RRM. noise corresponds to regularizer. variance parameters $\sigma^2, \tau^2$ correspond to regularization parameter $\lambda$.
**When to use what?**: different noise distributions and different parameter priors.
## Model comparison with significance test
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
## Principal Component Analysis
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
Kernel PCA: use kernel trick for non-linear principal components.
# Regression
## Least Squares Regression
**Goal**: find best-fitting linear function. $\min_{\tilde{w}}{\sum_{i=1}^{n}{\frac{1}{2}\left((\tilde{x}^{(i)})^{\top}\tilde{w}-y^{(i)}\right)^2}}$ or $\min_{\tilde{w}}{{\frac{1}{2}||\tilde{X}\tilde{w}-y||}^2}$.
**Bias integration**: into weights, $\tilde{x}$ column 1.
**Weights**: influence of each parameter on result.
**Offset**: general bias (or weight 0).
**Mean squared error (MSE)**: $L=\frac{1}{2}(y-\hat{y})^2$.
**Gradient**: $\nabla L=X^{\top}(Xw-y)$. Solve for 0: $(X^\top X)w=X^\top y$.
**Runtime**: $O(d^3)$.
**Intuition why there are always solutions**: minimising not eliminating loss -> always a solution.
## Polynomial regression and basis functions
**map to higher-dimension linear regression**: $x \to \tilde{x}=(x^d,x^{d-1},…,x,1)^\top\in \mathbb{R}^{d+1}$.
**mapping works for arbitrary function**: we can model anything theoretically. problem: over- and underfitting.
## More Regression
**Ridge regression**: least squares with 2-norm regulariser. solved via linear equations or gradient descent. Zero-ed gradient: $X^\top X+n\lambda I=X^\top y$.
**LASSO**: sparse solutions (example: many genes, few patients for data). $\min_w{\frac{1}{2n}||Xw-y||_2^2+\lambda||w_||_1}$.
**Elastic Net**: interpolation between ridge and lasso.
**Robust regression**: loss insensitive to outliers. $min_w\frac{1}{n}||Xw-y||_1$. often with different regularizer than 1-norm.
## Evaluation
**Mean squared error** $MSE=\frac1n\sum_{i=1}^n{(y_i-\hat{y}_i)^2}$. Penalise larger errors more than small ones. less interpretable due to square.
**Root mean squared error** $RMSE=\sqrt{MSE}$. improves interpretability over MSE.
**Mean absolute error** $MAE=\frac1n\sum_{i=1}^n{|y_i-\hat{y}_i|}$. more robust/less sensitive to individual errors.
**Coefficient of Determination** $R^2=1-\frac{\sum{(y_i-\hat{y}_i)^2}}{\sum{(y_i-\bar{y})^2}}$. 1 means perfect prediction, 0 means same as predicting the mean, negative means worse performance that constant predictor.
# Classification
## Binary Classification
*Predict yes or no, -1 or +1 $\to$ separate points by hyperplane (n-1 dimensional plane).*
**Intuitive loss function**: $l(y,\hat{y})=\begin{cases}0 & \text{if } y = \hat{y} \\ 1 & \text{if } y \neq \hat{y} \end{cases}$. NP-hard because of the jump in the loss function
	$\to$ not differentiable and thus no gradient.
## Logistic regression
*Use log loss instead $f(x)=\log{(1+\exp{(-y\cdot (x^\top w+b)}))}$.*
- **Misleading name**: No regression but actually classification.
- **Logistic function**: smooth approximation of the step function. $p(y=1|x)=\frac{1}{1+\exp{(-(x^\top w+b))}}$.
- **MLE**: Logistic regression is the MLE when using logistic function is used.
**More loss functions**: Hinge $max(0,1-t)$. Squared hinge loss $max(0,1-t)^2$.
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