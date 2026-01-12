---
disableComments: true
toc: false
math: true
title: What is DAS doing?
---

Here's my notes on what DAS is doing when they say "learn a rotation matrix", and how that's equivalent to the more Bau lab way of thinking about it, "learning a subspace." 
## Trivial concrete example 
Let's say your activations were in $\mathbb{R}^4$, where the standard basis is $e_1, e_2, e_3, e_4$. Say the subspace that was causally important for a given "foo" variable was spanned by $e_2$ and $e_3$, and DAS had perfectly learned that. Now, we want to intervene on a base hidden state $h_{base}$, setting its "foo" variable to whatever it was in $h_{src}$, where $$h_{base}=\begin{bmatrix}a\\\\ b\\\\ c \\\\ d\end{bmatrix}; h_{src}=\begin{bmatrix}e\\\\ f\\\\ g \\\\ h\end{bmatrix}$$
and then the desired intervened hidden state would be 
$$h_{intervened}=\begin{bmatrix}a\\\\ f\\\\ g \\\\ d\end{bmatrix}.$$

### DAS Viewpoint
DAS thinks about this in terms of an orthogonal rotation. In their codebase, to do an intervention, they apply the learned rotation $R$ to both $h_{src}$ and $h_{base}$ and then literally swap out the first $k$ entries of those hidden states (where $k$ is the dimension of the subspace learned). So the rotation matrix DAS would have learned in this case would be one that moves the relevant dimensions to the beginning of the vector:
$$R=\begin{bmatrix}
0 & 1 & 0 & 0 \\\\
0 & 0 & 1 & 0 \\\\
1 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 1 \\\\
\end{bmatrix} = 
\begin{bmatrix}
\text{--- } e_2^T \text{---} \\\\
\text{--- } e_3^T \text{---} \\\\
\text{--- } e_1^T \text{---} \\\\
\text{--- } e_4^T \text{---}
\end{bmatrix} \text{ so that } Rh_{base} = \begin{bmatrix}b\\\\ c\\\\ a \\\\ d\end{bmatrix}$$

Then, we can achieve $h_{intervened}$ by calculating $Rh_{base}$ and $Rh_{src}$, swapping out the first $k=2$ dimensions, and then rotating back. 

$$ h_{intervened} = R^{-1}(Rh_{base} \leftarrow_{:k} Rh_{src})$$

```python
 # In _do_intervention_by_swap() (pyvene/models/intervention_utils.py:115):
  if subspaces is None:
      if mode == "interchange":
          base[..., :interchange_dim] = source[..., :interchange_dim]
```

### Bau Lab Viewpoint
I've written this out before [here](https://sfeucht.github.io/blackboxnlp_abstract_2024.pdf). Instead of thinking of this as a rotation matrix, we could think of it as adding the projection of $h_{src}$ onto the relevant subspace to the projection of $h_{base}$ onto everything *except* for the relevant subspace. 

So here, let's define a matrix $A$, which has columns $e_2$ and $e_3$, which define the ground-truth subspace we want to intervene on. In general, to get a projection matrix onto the space spanned by columns of $A$, you'd want $A(A^TA)^{-1}A^T$, but since $A$ is orthogonal, we can simplify: $A^TA=A^{-1}A=I$ and so the projection matrix is just $P=AA^T$. 
$$P = \begin{bmatrix}
| & |  \\\\
e_2 & e_3  \\\\
| & | 
\end{bmatrix}
\begin{bmatrix}
\text{--- } e_2^T \text{---} \\\\
\text{--- } e_3^T \text{---} \\\\
\end{bmatrix} = 
\begin{bmatrix}
0 & 0 & 0 & 0 \\\\
0 & 1 & 0 & 0 \\\\
0 & 0 & 1 & 0 \\\\
0 & 0 & 0 & 0 \\\\
\end{bmatrix}$$

Now, if I want to project onto everything *but* the "foo" subspace, then I just need $I-P$. 
$$I - P = \begin{bmatrix}
1 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 1 \\\\
\end{bmatrix}$$

Why does this project onto "everything but the 'foo' subspace"? If you work it out for a single hidden state $h$, you can see that $(I-P)h + Ph = h$. 
The intervention itself can just be thought of as swapping out one of these terms:
$$h_{intervened}=(I-P)h_{base} + Ph_{src},$$
which actually looks very intuitive if you write it out for our concrete example:
$$\begin{bmatrix}
1 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 0 \\\\
0 & 0 & 0 & 1 \\\\
\end{bmatrix}\begin{bmatrix}a\\\\ b\\\\ c \\\\ d\end{bmatrix} + 
\begin{bmatrix}
0 & 0 & 0 & 0 \\\\
0 & 1 & 0 & 0 \\\\
0 & 0 & 1 & 0 \\\\
0 & 0 & 0 & 0 \\\\
\end{bmatrix}\begin{bmatrix}e\\\\ f\\\\ g \\\\ h\end{bmatrix}=
\begin{bmatrix}a\\\\ 0\\\\ 0 \\\\ d\end{bmatrix} + \begin{bmatrix}0\\\\ f\\\\ g \\\\ 0\end{bmatrix}=h_{intervened}$$