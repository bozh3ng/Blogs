Principal Component Analysis (PCA) is a dimensionality reduction technique, and transforms correlated features into a new set of uncorrelated variables called Principal Components (PCs)

# Data in the frequentists' perspective
Note: PCA is an unsupervised method, so when we say 'data matrix', it is the same as 'feature matrix' in the supervised method

Imagine we have a real data matrix $X$ with $n$ rows and $d$ columns (shape $n\times d$) , where each row $i\in[n]$ is an sample from experience(sampling process), each column $j\in[d]$ is a feature which can be seen as a (one dimensional) **random variable** over $n$ samples. 

What this means?

Recall that a random variable is a function that maps the sample space to the real numbers. 

$$\mu: \Omega \longrightarrow \mathbb{R}$$

In this case, each row is a sample from the sample space: $X_i \in \Omega$ , each column maps rows to a real number (the entries in the data matrix) : 

$$\mu_j\left(X_i\right)\in\mathbb{R}$$

The entries in the data matrix describe the behavior of each random variable (column). If we have infinite samples, we have the law of random variables.

A $n \times d$ data matrix is multiple realizations of $d$ random variables; the sample size $n$ is not really important, it can be large or small, but it is ruled by the random variable. The $j$-th column then collects the realizations of the random variable $\mu_j$.

Each random variable has a mean and a variance. If two random variables are not independent, we describe their connection using covariance.

Consider $n \times d$ centered data matrix $X$, the **covariance matrix** of these $d$ features is given by

$$  
C=\frac{1}{n-1} X^T X  
$$

It has shape $d\times d$, which means the covariance of pairwise features across all samples  

# Principal Component Analysis (PCA)
PCA finds orthogonal directions $\mathbf{w}_1, \ldots, \mathbf{w}_p$ that maximise the projected variance for $C$. These directions are the eigenvectors of $C$, and the corresponding eigenvalues give the variance captured by each principal component:

$$  
C{w}_i=\lambda_i {w}_i, \quad \lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_p \geq 0  
$$

The main task of PCA is to calculate eigenvectors and eigenvalues of $C$

# Singular Value Decomposition (SVD)  
The method we implement PCA in practice

Decompose data using SVD:

$$X=U \Sigma V^T$$

The columns of $V$ are the eigenvectors of $X^T X$, or the matrix of **principal axes**

In PCA, each column of $V$ is a direction in the feature space $\mathbb{R}^d$. These directions are the principal axes along which the data $X$ has maximum variance.

When we calculate $X V$, we take each row of $X$ (sample, or an observation in $\mathbb{R}^d$ ) and express it in the new coordinate system defined by the columns of $V$. This is precisely the principal component projection $ T=XV$. 

$$T=X V=U \Sigma V^T V=U \Sigma$$

The matrix $T$ is called the **score matrix**, it contains **principal component scores**.

**Principal component scores** are the coordinates of each observation in the new (principal component) basis. The first column of $T$ is the coordinate along the first principal component (the direction of greatest variance)

For dimension reduction, we consider the matrix $V_L$ that contains the first $L$ columns of $V$. The first column of $V$ is the direction where data have maximal variance, the second column of $V$ is the direction of the second maximal variance, perpendicular to the first direction.

The truncated score matrix is 

$$T_L=X V_L$$

$T_L$ has a lower dimension than the original data matrix $X$; this is what we expect from PCA.  
In machine learning, we can use it to train the model. For test dataset $X_{test}$, we do the same PCA process $X_{test}V_L$  

# Why it works?
PCA maps data to its maximal variance direction. But why use the largest variance direction? 

If data is not random, it means it has large eigenvalues and small eigenvalues, a large eigenvalue corresponding to a large variance. 

**Assumption**: Directions of small variance can be dominated by noise, our true data live in a lower dimensional subspace. 

PCA drops low-variance features and keeps high-variance features. For high-variance features, PCA also mixes (linearly combines) these features into principal components, making them orthogonal.

Note: when PCA drops low-variance dimensions, it is only dropping directions that appear less informative in terms of $X$; there is no guarantee about how those dimensions relate to the label $y$

If features are nearly independent, the covariance matrix is close to a diagonal matrix, and the eigenvalue roughly equals that feature’s variance, PCA finds that each principal component just corresponds (mostly) to each individual feature. In this case, PCA will not contribute a lot (but independent is a good property)

If features are highly dependent, the covariance matrix is close to an off-diagonal matrix; this case is suitable for PCA. PCA merges linearly dependent (for example, multiple Gaussian distributions) into a principal component. It can not merge a non-linear relation.  


