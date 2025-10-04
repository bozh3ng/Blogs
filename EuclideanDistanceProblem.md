# Matrix as a Linear Transformation
A real matrix
$$
M \in \mathbb{R}^{d \times n}
$$
encodes a linear map
$$
T_M: \mathbb{R}^n \longrightarrow \mathbb{R}^d, \quad x \mapsto M x .
$$

The map can collapse dimensions.
The rank $r=\operatorname{rank}(M)$ is the number of linearly independent columns (or rows).
- Column space (image) $\mathcal{C}(M)=\left\{M x \mid x \in \mathbb{R}^n\right\} \subseteq \mathbb{R}^d$ is an $r$-dimensional subspace.
- Null space (kernel) $\mathcal{N}(M)=\left\{x \in \mathbb{R}^n \mid M x=0\right\}$ has dimension $(n-r)$.

So although inputs live in $n$ dimension, only an $r$-dimensional slice survives after the transformation.

If we perform SVD on $M$ :
$$
M=U \Sigma V^T
$$

$V^T$ (or equivalently, $V$ ) is an **orthogonal matrix** $\left(V^T V=I\right)$ with shape $n\times n$,  it represents 
- pure rotation ($\det=1$, $SO$ group), 
- rotation and reflection ($\det=-1$)

$V^Tx$: rotate $x$ 

$\Sigma$ is a descending **singular values diagonal matrix** ( $\sigma_1 \geq \sigma_2 \geq \ldots$ ). It has same rank $r$, means *stretch* along the principal axes.
- Components aligned with the singular directions are stretched or compressed by $\sigma_i$.
- Components orthogonal to these directions are completely eliminated (mapped to zero).

$\Sigma V^Tx$: stretch $V^Tx$ along $r$ dimensions, and possible reduce dimensions(project from $\mathbb{R}^n$ to $\mathbb{R}^d$) 

$U$: another **orthogonal matrix**, but in $\mathbb{R}^d$ 

An eigenvector of a matrix $A$ is a special vector that remains in the same direction (or is reversed) when transformed by $A$:
$$
A \mathbf{v}=\lambda \mathbf{v}
$$
It means the invariant direction under transformation matrix $A$ , or principal directions
A zero eigen $\lambda$ and its eigen vector $v$ means the matrix maps direction $v$ to zero.  

# Positive semidefinite (PSD)  ($S_{+}^n$)
The following statements are equivalent:
- The matrix $A \in S^n$ is positive semidefinite $(A \succeq 0)$.
- For all $x \in \mathbb{R}^n, x^T A x \geq 0$.   (But generally it's impossible to check all $x$)
- All eigenvalues of $A$ are nonnegative.
- All $2^{n-1}$ principal minors of $A$ are nonnegative.
- There exists a factorization $A=B^T B$.

# Euclidean distance problem
Consider $n$ points each points with dimension $d$: 
$$x_1, \ldots, x_n \in \mathbb{R}^d$$
Can a set of points be identified uniquely from all the *pairwise distances* between them?
Yes, and these points are equivalence under **rigid transformation**

## Gram matrix
For data matrix $X\in \mathbb{R}^{d \times n}$, 
$$\tilde{G}:=X^TX\in\mathbb{R}^{n\times n}$$
Thus $\operatorname{rank}(\tilde{G})=\operatorname{rank}\left(X^T X\right)=\operatorname{rank}(X)=d$
REMARK: Gram matrix is PSD

Given $D^{(2)} \in \mathbb{R}^{n \times n}$ be pointwise squared distance matrix . $D^{(2)}$ is symmetric($S^n$), but not necessary PSD 

## Geometric centering matrix
$$
J=I_n-\frac{1}{n} \mathbb{1}\mathbb{1}^T
$$
where $I_n$ is the $n \times n$ identity matrix and $\mathbb{1}$ is the vector of ones.
REMARK:  $\operatorname{rank}(J)=n-1$ 

According to classical multidimensional scaling (cMDS), Gram matrix:
$$\tilde{G}=-\frac{1}{2} J D^{(2)} J$$

Recall gram matrix is defined as $\tilde{G}:=X^TX\in\mathbb{R}^{n\times n}$, so our goal is to find a $\hat{X}$ has structure  $\tilde{G}=\hat{X}^T \hat{X}$.  In this case,  $\hat{X}$ is rigid of original points 

Compute the eigendecomposition 
$$\tilde{G}=Q \Lambda Q^{-1}$$
Because $\tilde{G}$ is PSD, it eigen values greater than 0 . 
$$\lambda_1 \geq \lambda_2 \geq \ldots \geq \lambda_n > 0$$

Recall Gram matrix $\tilde{G}$ has rank $d$ , so we have $\lambda_1$ to $\lambda_d$ 

Define a square root diagonal matrix:
$$\Lambda_d^{1 / 2}:=\left[\operatorname{diag}\left(\sqrt{\lambda_1}, \ldots, \sqrt{\lambda_d}\right), 0_{d \times(n-d)}\right]^T$$
We can write gram as 
$$\tilde{G}=Q \Lambda Q^T=\left(Q \Lambda^{1 / 2}\right)\left(\Lambda^{1 / 2} Q^T\right)$$
So
$$\hat{X}=Q \Lambda_d^{1 / 2}$$


