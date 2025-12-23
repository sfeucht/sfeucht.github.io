---
disableComments: true
toc: false
math: true
title: Notes on Geometry Papers
---

# Not All LM Features are 1D Linear (Engels et al., 2024)
[[Paper](https://arxiv.org/pdf/2405.14860), [Video](https://www.youtube.com/watch?v=eVlGeHA2Cnw&t=858s)] - They're basically trying to figure out how to decompose hidden states into sums of different functions of the input (features). So for example, you might have a 1-dimensional representation of an integer value 3, added to an n-dimensional representation of the language semantics of "three," etc. 

When you're doing this, there's a problem: how do you know whether a multi-dimensional feature you've found is "atomic", or whether it's actually possible to further decompose it into other sub-features? 

## Reducibility
To figure this out, they formally define *reducible* features—which crucially we don't actually want to count as a good/valid multi-dimensional feature. So for a given multi-dimensional feature $\bf f$ (defined as a function that maps from inputs to some $d_f$-dimensional subspace), can it actually be "broken down" (e.g. latitude and longitude)?

They come up with two metrics to see if this is approximately true:
1. $S(f)$ - **Separability index.** For all possible ways to break down a feature into $\bf a$ and $\bf b$, what is the minimum mutual information $I(\textbf{a}, \textbf{b})$? For example, a multidimensional Gaussian will not actually have mutual information between subfeatures if you choose the right axes. Higher = harder to separate.
2. $M_\epsilon(f)$ - **$\epsilon$-mixture index.** Across all the token positions, can we pick a special vector $\bf v$ for which the feature can be projected near zero pretty often? (in practice, this is something like less than $\epsilon$ * standard deviation rather than zero). If you can find a vector $\bf v$ and offset $c$ so that $\textbf{v} \cdot \textbf{f(t)} + c$ is small for lots of token positions, then that means that in all of those cases that direction in the feature space wasn't really being used. Of course, $\bf v$ has to be within the subspace $\mathbb{R}^{d_f}$, because otherwise you could easily find a vector that's orthogonal to $\mathbb{R}^{d_f}$ and zeros out everything. Higher = easier to separate. 
 <details>
<summary>Concrete-ish example of mixture index</summary>
Let's say your multi-dimensional feature $\bf f$ was dimension $d_f=2$ but to your dismay it was actually a mixture of two features, $\bf e_1$ and $\bf e_2$. For 60% of the token positions where the feature is active, it's using mostly $\bf e_1$, and for the other 40% it's using mostly $\bf e_2$. In such a case, you could choose $\bf v=e_2$ and get a zero dot product for 60% of tokens and one dot product for the other 40%, resulting in a score of around 0.60. This is pretty high, and it indicates that this so-called "multi-dimensional feature" is actually just a combination of sub-features represented by $\bf e_1$ and $\bf e_2$.
</details>

In practice, $S(f)$ scores for GPT-2 features are mostly less than 0.2 (aka, most features are pretty separable), and $M_\epsilon(f)$ features are quite high, mostly bigger than 0.4 (aka, most features are pretty much mixtures). They use these scores to argue that their day-of-week features, since they have high $S(f)$ and low $M_\epsilon(f)$, are irreducible multi-dimensional features. 

## Going from SAE to Multi-Dim Features
If $\bf D$ is the decoder matrix of the SAE containing all of the output features, then to cluster features together, they take the cosine similarity between all decoder vectors and prune away cosine similarities below a threshold $T$. By construction these clusters will be "$T$-orthogonal" (i.e. if $T=0$ then they're truly orthogonal). 

If the SAE is good at reconstructing, then when a multi-dimensional non-reducible feature $\bf f$ is active, **they claim that one of these cosine-similar clusters will be equal to f.** This is not super obvious. Naively, you'd think it'd be the opposite—that if $\bf f$ was a 2D feature that was properly reconstructed by the SAE, the SAE would have learned two orthogonal decoder vectors that span the space (and those would have close to zero cosine similarity). But if $\bf f$ is truly a multi-dimensional feature, it would never make sense to separate out these two features; then the SAE would get penalized by always having both features active whenever it needs to reconstruct $\bf f$. So instead, they guess that the SAE would learn a bunch of cosine-similar things that are all in $\bf f$ (intuitively, maybe this would be like learning separate "Monday", "Tuesday", "Wednesday" features). 

So what they do is:
1. Cluster all the SAE decoder vectors using this thresholding thing
2. To analyze a cluster, get cluster-specific reconstructions of all hidden states $\textbf{x}_{i,l}$.
3. Analyze that cluster's representations across a bunch of hidden states by looking at PCA projections, or running $S(f)$ and $M_\epsilon(f)$

Two important details: 
- In order to calculate these scores, they actually *first* calculate the PCA directions over the reconstructed activations, and then project onto PCA components 1-2, 2-3, 3-4, 4-5, averaging the separability/mixture over each of these planes.
- This process implicitly filters for datapoints that are relevant for this cluster/feature. In step (2), if none of the cluster's features are active for a particular hidden state $\textbf{x}_{i,l}$, it is not included in the analysis. In the case of a days-of-the-week feature, the PCAs will of course look pretty nice, since the biggest variation between a bunch of weekday vectors will almost surely be information about weekday.

Another cool thing is that they show that these features are actually cones, where the first principal component seems to be intensity of weekday-ness, perhaps. 

![](/geometry/engels_pca.png)

## Intervening on Circles 
While they do try intervening on the subspace found by the SAE, they get slightly better results by training probes to find good subspaces at each layer. Specifically, they 
1. Take the top-$k$ principal component directions of hidden states at the "Monday" position (pretty sure this position) across all the prompts and project onto there first.
2. Then train a linear probe $\bf P$ in that space that maps from $k$ to 2 dimensions, trained to correspond to <tt>circle</tt>($\alpha$) -- e.g. for weekdays <tt>circle</tt>$(\alpha)=[\cos(2\pi\alpha/7), \sin(2\pi\alpha/7)]$. 
3. To intervene on "Monday" and make it look like "Wednesday", they just discard "Monday." I am confused about how exactly this intervention works, because their Equation 6 seems wrong (you can't calculate <tt>circle</tt>$(\alpha_{j'}) - \overline{x\_{i,l}}$ directly because they are different dimensions). Equation 7 doesn't clarify, it seems to have a missing parenthesis. 

<!-- Start with mean over prompts $\overline{x_{i,l}}$. Project that onto the circle with $\textbf{PW}_{i,l}$ and then calculate offset from <tt>circle</tt>(Wednesday). Then project that offset back to model space with $\textbf{W}^T\_{i,l}\textbf{P}^+$ and add back to the mean to get final activation.  -->
Josh Engels mentions in the talk that the intervention only works if you ablate out everything else that's not in the PCA; I'm not exactly sure what he means here, probably the fact that they have to mean-ablate everything by using $\overline{x\_{i,l}}$ instead of the base activation. 

## Generic Ideas/Takeaways
- How does the model actually use these circular representations to calculate the answer? 
- Some of these facts must be piecewise memorized as well (e.g. Saturday is 1 day after Friday is almost surely memorized) -- probably why they have to ablate all other weekday information. 
- Presumably lots of weekday embedding information is unrelated to circles -- if you rotated within the circle subspace for tasks like "What holidays are typically on [Thursday]?" or "What letter does [Thursday] start with?" then you'd probably see it doesn't affect anything. 
- It still worries me to think about multiple circles happening at once. If you have six orthogonal 2D circles, could that just be some alternate formulation of an n-dimensional subspace? 