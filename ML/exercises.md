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
## 3. Polynomial Regression

## 4. Regularisation

## 5. Maximum Likelihood Principle

## 6. More Regression

## 7. Logistic Regression

## 8. SVM

## 9. Decision Trees

## 10. Discriminant Analysis

## 11. k-means

## 12. PCA

## 13. Dimensionality Reduction

## 14. Matrix Factorisation

## 15. Deep Learning

