---
disableComments: true
toc: false
math: true
title: Circle Math
---

## Rotations and Complex Eigenvalues

Whenever a matrix performs a rotation (other than an angle of $0$ or $\pi$), it has complex eigenvalues. This is because you can't ever find any (real) vector that will stay in the same place after a rotation by some non-nice angle. Let's think about a 2D rotation matrix, which looks like

$$R(\theta) = \begin{bmatrix}
\cos\theta & -\sin\theta \\\\
\sin\theta & \cos\theta
\end{bmatrix}$$

where its eigenvalues solving the characteristic polynomial are $\lambda=\cos\theta \pm i\sin\theta$. If the matrix itself is real, these imaginary eigenvalues will always come in conjugate pairs. When you allow yourself to use complex numbers, it becomes possible to get $\lambda$ and $v$ such that $Rv = \lambda v$ even though this is a rotation. Try working out $\lambda=\cos\theta + i\sin\theta$ and $v=[1, -i]^T$ to convince yourself of the fact that this works. 

<details>
<summary>(If you don't actually want to work this out for yourself)</summary>
$$\begin{bmatrix}
\cos\theta & -\sin\theta \\
\sin\theta & \cos\theta
\end{bmatrix}\begin{bmatrix}
1 \\
-i
\end{bmatrix} = (\cos\theta + i\sin\theta)\begin{bmatrix}1 \\ -i\end{bmatrix} $$
$$\begin{bmatrix}
\cos\theta + i\sin\theta \\
\sin\theta - i\cos\theta
\end{bmatrix} = \begin{bmatrix}\cos\theta + i\sin\theta \\ -i\cos\theta + \sin\theta\end{bmatrix} $$
</details>

I never really realized this, but rotations are deeply two-dimensional, tied up with the dualness of complex numbers. If you have a rotation in higher dimensions, it's actually constrained to a 2D plane, or multiple 2D planes if we're more than three dimensions. For now, if you think of any rotation in 3D, it's actually always a rotation in a 2D subspace, with an extra axis orthogonal to the plane that the vector is rotated on. Literally imagine any rotation in 3D and there's always a "spoke" that's being rotated around. Concretely, if we have vectors $[x,y,z]$, then a rotation by an angle of $\theta$ around the x-axis (on the yz plane) would look like:

$$R(\theta)= \begin{bmatrix}
1 & 0 & 0 \\\\
0 & \cos\theta & -\sin\theta \\\\ 
0 & \sin\theta & \cos\theta 
\end{bmatrix}$$

where one eigenvector $\lambda=1,v=[1, 0, 0]^T$ would correspond to anything that's on the x-axis (which stays put) and the other two eigenvectors are $\lambda=\cos\theta\pm i\sin\theta,v=[0,1,\pm i]^T$. Now, here's a fact: the real and imaginary parts of these eigenvectors precisely show that the rotation is on the yz-plane. In general, if you have a pair of two complex eigenvectors describing a rotation, then the plane that's being rotated on is always going to be the span of $\text{Re}(v), \text{Im}(v)$. We can see that clearly here:

$$v=\begin{bmatrix}0 \\\\ 1 \\\\ -i \end{bmatrix}=\begin{bmatrix}0 \\\\ 1 \\\\ 0 \end{bmatrix}+i\begin{bmatrix}0 \\\\ 0 \\\\ -1 \end{bmatrix}$$

where the real part of $v$ is the y-axis, and the imaginary part is the z-axis, matching up with the fact that we defined this rotation to be on the yz-plane. The reason why this is true in general: let's say you have complex eigenvector $u + iw$ and eigenvalue $\alpha + i\beta$. If you expand out the multiplication in terms of the real and imaginary parts of these eigenvectors/values... 

$$R(u + iw) = (\alpha + i\beta)(u + iw) $$
$$Ru + iRw = \alpha u + i\alpha w + i\beta u + i^2\beta w$$
$$Ru + iRw = (\alpha u - \beta w) + i(\alpha w + \beta u)$$
$$Ru  = (\alpha u - \beta w) $$
$$Rw = (\alpha w + \beta u)$$


you get these two equations, which tell you that applying our rotation to the real part of the eigenvector $u$ will always give some linear combination of $u,w$, and applying our rotation to the imaginary part of the eigenvector $w$ will also give some linear combination of $u,w$. This is another way of saying that the rotation matrix $R$ will never move the vectors $u$ or $w$ off that $u,w$ plane; it's always rotating them inside the $u,w$ plane. Therefore, if we have a conjugate pair of eigenvectors for a given transformation, then we can read out the exact 2D plane within which that transformation rotates just by looking at the pair's real and imaginary components.

<details>
<summary>Bonus: reading off the angle/scaling by looking at eigenvalue</summary>
The angle that $R$ rotates by is given by $\theta=\arctan(\beta/\alpha)$. In other words, this is crazily telling us that you can just plot the eigenvalue on the complex plane and look at what angle it is, and that tells you by what angle $R$ is rotating in the corresponding subspace. Plus, if you calculate $|\lambda|=\sqrt{\alpha^2+\beta^2}$, that is actually the radius $r$ of the eigenvalue on the complex plane, and is also the amount by which the transformation scales the vector it rotates.
</details>


I was able to get away with not thinking about complex eigenvalues for a long time probably because I was mostly looking at covariance matrices and stuff, which are symmetric and are guaranteed to have real eigenvalues. But actually, just like how if you randomly sampled a matrix it would almost surely be full-rank, it would also almost surely be some kind of stretch + rotation, giving it complex eigenvalues. 

## Rotations in 4D+

If a rotation in 3D is within a 2D plane with a third-dimension "spoke" that's orthogonal to that plane, then what is rotation in four dimensions? Thinking in terms of eigenvectors, you can always decompose a rotation in four dimensions into two rotations in two orthogonal 2D planes (two pairs of conjugate eigenvalues).[^1] Because it's impossible to imagine a four-dimensional space, I'll think of it as some kind of control panel with two dials that can be twisted independently of each other. 

In this "dial" analogy, each dial is a 2D subspace that's orthogonal to the other dials. Any given vector can be projected onto each of these subspaces to see where those dials are "currently" pointing, specifying that vector. Then, if you multiply that vector by a rotation matrix (the one whose eigendecomposition gave you those dial planes in the first place), then it will rotate each of those dials by a different $\theta$, where that $\theta$ is exactly specified by the complex eigenvalue for that plane like we talked about above.

By the way, you could of course always *compose* rotations in two non-orthogonal planes that are not orthogonal to each other, even in 3D, which is a really messy thing. I'm still not sure if we need to consider that for our work. But at least when we are decomposing, there's always a way to have a bunch of orthogonal 2D planes.

[^1]: When I asked Claude to give me feedback on these notes, it said that actually any real orthogonal matrix in even dimensions can be block-diagonalized into 2x2 rotation blocks, which it called the Schur decomposition. In the case of orthogonal matrices, which are normal, the Schur decomposition is the eigendecomposition, so I think this can be safely ignored for now. 