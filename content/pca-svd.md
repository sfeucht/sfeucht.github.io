---
disableComments: true
toc: false
math: true
title: Easy way to calculate PCA
---
Let's say you have a matrix $A$ of dimension (model_dim, n_samples), i.e. the columns correspond to points in a dataset. If we want to calculate PCA, we first center by subtracting the mean of the columns of $A$. 

The classic PCA approach is to then get the covariance matrix $AA^T$ and take its eigendecomposition. From [other notes](/Covariance_and_Whitening_Self_Explanation.pdf) we know that since the covariance matrix is symmetric, the eigendecomposition is equivalent to the SVD. So we have $U_{AA^T}\Sigma U_{AA^T}^T$ where my ugly subscripts are to be very clear that these are the singular vectors/eigenvectors of the covariance matrix; we can use the same matrix on both sides because it's symmetric and it's also an eigendecomposition. 

We don't actually have to calculate $AA^T$. We can directly take the SVD of $A$ instead as $U_A\Sigma V_A^T$. Then, we know that $AA^T=(U_A\Sigma V_A^T)(V_A\Sigma U_A^T)=U_A\Sigma^2U_A^T$ and that the left singular vectors of the data matrix $A$ are the same as the eigenvectors of $A$'s covariance matrix. 

If you ever get confused about rows and columns, remember that you'd always want to take the singular vectors that are the model dimension; in this case they are the left singular vectors, since $A$ is (model_dim, n_samples). Also, the covariance matrix has to be (model_dim, model_dim).

# Another note, which should have been obvious?
If the columns of $A\in\mathbb{R}^{(d,n)}$ are all orthogonal vectors, then $AA^T$ is also the matrix that projects activations onto the $n$-dimensional subspace spanned by columns of $A$. (If they were not orthogonal vectors, the projection matrix would be $A(A^TA)^{-1}A^T$.) I can't believe I never noticed this until now, need to think about deeper connections here.

There's two ways to "project onto a subspace." There's the linear algebra 101 thing, where a matrix multiplication is a change of basis: so if I have a vector $v\in\mathbb{R}^d$ and multiply $A^Tv$, then that takes dot product of $v$ with each column of $A$, telling me "how much" that vector is in the direction of each of those columns (e.g. [0.2, 3.1]). We can reconstruct $v$ by just multiplying those coefficients by the columns of $A$ again: $A(A^Tv)$. But wait, we've actually lost information now about anything that *can't* be spanned by the columns of $A$. That's why $AA^T$ works as a projection matrix, if you want to *only* get the information in $v$ that's in the subspace spanned by $A$'s columns, but keep that information in $d$ dimensions. 