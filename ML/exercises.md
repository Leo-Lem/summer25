[[ML/exercises.pdf|exercises]]
## 0. Repeat Linear Algebra
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
## 1. Least Squares Regression
**Goal**: find best-fitting linear function. $\min_{\tilde{w}}{\sum_{i=1}^{n}{\frac{1}{2}\left((\tilde{x}^{(i)})^{\top}\tilde{w}-y^{(i)}\right)^2}}$ or $\min_{\tilde{w}}{{\frac{1}{2}||\tilde{X}\tilde{w}-y||}^2}$.
**Bias integration**: into weights, $\tilde{x}$ column 1.
**Weights**: influence of each parameter on result.
**Offset**: general bias (or weight 0).
**Mean squared error (MSE)**: $L=\frac{1}{2}(y-\hat{y})^2$.
**Gradient**: $\nabla L=X^{\top}(Xw-y)$. Solve for 0: $(X^\top X)w=X^\top y$.
**Runtime**: $O(d^3)$.
**Intuition why there are always solutions**: minimising not eliminating loss -> always a solution.
## 2. Optimisation for ML
**gradient**: partial derivates.
**convex sets**: all points are connected with other points.
**convex functions**: convex set and connection is contained in shape.
**convexity rules**: linear is convex and concave. norm is convex. square is convex if $A$ is psd ($w^TAw$).
**exact line search for step length/learning rate**: if i move only along given line, how far should i move to minimise?
## 3. Polynomial regression and basis functions
**map to higher-dimension linear regression**: $x \to \tilde{x}=(x^d,x^{d-1},…,x,1)^\top\in \mathbb{R}^{d+1}$.
**mapping works for arbitrary function**: we can model anything theoretically. problem: over- and underfitting.
## 4. Over-/Underfitting
**$k$-fold cross validation**: split data into blocks, use each block for validation once and others for training (train $k$ times).
**regularization**: constrain magnitude/norm of model parameters. $\min_w{L(w)+\frac{\lambda}{2}||w||_2^2}$.
**approach**: solve for many $\lambda$, k-fold cross validation for each (called regularization paths), pick best $\lambda^*$ (minimal validation error), train with $\lambda^*$.
**Empirical (ERM) v. regularized risk minimization (RRM)**: without and with regularization.
**Bias v. variance**: TODO
## 5. More Regression
**Ridge regression**: least squares with 2-norm regulariser. solved via linear equations or gradient descent.
**LASSO**: sparse solutions (example: many genes, few patients for data). $\min_w{\frac{1}{2n}||Xw-y||_2^2+\lambda||w_||_1}$.
**Elastic Net**: interpolation between ridge and lasso.
**Robust regression**: loss insensitive to outliers. $min_w\frac{1}{n}||Xw-y||_1$. often with different regularizer than 1-norm.

