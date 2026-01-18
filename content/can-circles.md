---
disableComments: true
toc: false
math: true
title: Can's Weekday Circles Notebook
---

## Complex Eigenvalues

Whenever a matrix performs a rotation (other than $0$ or $\pi$ degrees), it has complex eigenvalues. This is because you can't actually find any (real) vector that will stay in the same place after a rotation by some non-nice angle. Let's think about a 2D rotation matrix, which looks like

$$R(\theta) = \begin{bmatrix}
\cos\theta & -\sin\theta \\\\
\sin\theta & \cos\theta
\end{bmatrix}$$

where its eigenvalues solving the characteristic polynomial are $\lambda=\cos\theta \pm i\sin\theta$. Since the matrix itself is real, these imaginary eigenvalues come in pairs. If you plot these $\lambda$ on the complex plane, where the y-axis is $i$, then it is quite obviously on the unit circle of that imaginary plane; apparently, this unit-circle-ness is because it's an orthogonal transformation that does no stretching. 

Since the eigenvalues are complex, the eigenvectors have to be too. But our complex eigenvectors all come in pairs, where one is a complex conjugate of the other. 

Since most matrices are some combination of rotation and scaling, a randomly-generated matrix will almost surely have complex eigenvalues. However in practice we mostly look at symmetric matrices, like covariance matrices, Hessians, etc, which makes complex eigenvalues feel unfamiliar. 
