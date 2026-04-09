---
disableComments: true
toc: false
math: true
title: Neel's Modular Arithmetic Model 
---

They focus on a mod 113 model, finding key frequencies $k\in\\{14,35,41,42,52\\}$. How do they find these key frequencies?

They do a lot of analysis on the "neuron-logit map," $W_L\in\mathbb{R}^{|V|\times n}$, which is just the final MLP's $W_{down}$ multiplied with $W_{unembed}$. Here, $|V|=113$ is the vocab size, and $n$ is the number of MLP neurons. This is I think the most relevant place where they find the key frequencies. 
- They do this by taking the discrete Fourier transform "across the logit axis," i.e. from $\mathbb{R}^{|V|\times n}\rightarrow\mathbb{C}^{p\times n}$, where $p$ is the maximum period. Actually, $p=|V|$ as you can't differentiate any periods that are greater than the number of numbers we have, but I'll name them differently because they're conceptually different. 
- So now we have a bunch of $n$-dimensional rows. Since they are complex numbers, this means each row actually gives us two vectors: the real part gives the cosine vector in neuron space for this periodicity $u_k\in\mathbb{R}^n$, and the imaginary part gives the sine vector in neuron space $v_k\in\mathbb{R}^n$. See [my notes on rotations](/circles) for why. 

Most of the frequencies actually don't matter, so the $n$-dimensional row corresponding to that frequency will have a very small norm. This is exactly what their Figure 3b shows: the only rows with substantial norms are their key frequencies. 

If it really is the case that $W_L$ basically just uses five frequencies to represent output numbers, then their claim about how to approximate it using trig functions makes sense. As you scan over the output vocabulary (i.e., every possible output number), we can imagine each $u_k,v_k$ vector oscillating back and forth at a different frequency; this is what the DFT found by definition. The exact way that each vector oscillates is given by their $\cos(w_k),\sin(w_k)\in\mathbb{R}^{|V|}$, where the $c$th entry of e.g. $\cos(w_{42})$ is simply $\cos(42c(2\pi/113))$.

TODO you were here, work out explanation for $\cos(2\pi kc/p)$ 

$$W_L = \sum_{k\in\\{14,35,41,42,52\\}}$$