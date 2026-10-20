---
layout: single
title: "Initial impressions - Previous work"
date: 2026-10-20 15:00:00 +0200
tags:
  - Initial-Impressions
author: alexander
---

**Author:** {{ site.data.authors[page.author].name }}

Before we can appreciate what ideas are new in the preprint, we need to understand the context of previous work. This is the goal of this second post. I will also use this opportunity to tell a cohesive story with outlines of a few key proof ideas in the literature. This may be of independent interest, as a similar review of the subject has not previously been available.

**Table of contents:**
1. Generalized spectrum
2. Deterministic sufficient conditions
3. Probabilistic theory using random algebraic objects
	1. Toy case: walk matrices of digraphs with multiple edges
	2. Exploiting $\mathbb{Z}[x]$-module structure
	3. Undirected graphs
4. Large prime estimates
5. Boosting the probability using fixed-level estimates
6. Conclusion: an outline of a strategy

## Generalized spectrum

The term *graph* is reserved in this post for finite undirected graphs. Directed graphs will explicitly be referred to as digraphs.

We do *not* assume that the graphs are simple. Self-loops and multiple edges are permissible. Let me warn that many of the references that I will mention are stated for simple graphs. The key points for my story, however, extend to the general setting, and the flexibility of allowing loops will be useful in some places.

**Definition 1.** Two graphs $$G$$ and $$H$$ are *generalized cospectral* if their adjacency matrices have the same characteristic polynomial, and their complement graphs also have the same characteristic polynomial. We say that $$G$$ is *determined by its generalized spectrum (DGS)* if all generalized cospectral graphs $$H$$ are in fact isomorphic to $$G$$.

This notion dates back to Johnson and Newman ([1980](https://doi.org/10.1016/0095-8956(80)90058-1)), who arrived at it from a different direction. Their paper started from the perspective that the choice to take entries $$0$$ and $$1$$ in the usual adjacency matrix was somewhat arbitrary, and investigated what happens if one uses formal symbols $$x$$ and $$y$$ instead. They proved that the $$xy$$-adjacency matrices $$A^{x,y}_G$$ and $$A_H^{x,y}$$ have the same spectrum for every choice of $$x,y\in\mathbb{R}$$ if and only if the graphs are generalized cospectral!

Johnson and Newman also proved different equivalent formulations. One of these is relevant for our story. Let $$e=(1,\ldots,1)^T$$ be the all-ones vector, with the dimension matching the number of vertices $$n$$ in $$G$$.

**Theorem 2. (Johnson and Newman, 1980)** *Two graphs $$G$$ and $$H$$ have the same generalized spectrum if and only if there exists an orthogonal matrix $$Q\in\mathbb{R}^{n\times n}$$ satisfying $$Qe=e$$ that relates their adjacency matrices by conjugacy $$QA_GQ^T=A_H$$.*

It is not difficult to check that the existence of such an orthogonal matrix implies generalized cospectrality. The opposite direction requires an argument, omitted here for brevity.

**Remark 3.** The role of the all-ones vector is partly for aesthetic reasons. Up to scalar multiplication, it is the only nontrivial vector that is canonically defined. Given a different integer vector $$\xi\in\mathbb{Z}^n$$, one can also define a notion of cospectrality for the bivariate characteristic polynomial $$\Phi_G\in\mathbb{Z}[\lambda,t]$$ defined by $$\Phi_G=\det(\lambda I-A_G+t\xi\xi^T)$$. Much of the theory can be extended to this setting if one replaces the all-ones vector by $$\xi$$. Details and references can be found in [arXiv:2511.19625](https://arxiv.org/abs/2511.19625).

## Deterministic sufficient conditions

While it is clear that generalized cospectrality is more restrictive than ordinary cospectrality, it is not clear how specifically this additional information would make it easier to prove that a given graph is determined by its generalized spectrum. The equivalent definitions of Johnson and Newman still all make reference to the candidate cospectral graph. Hence, to show that $$G$$ is determined by its generalized spectrum, one has to enumerate all other potential graphs $$H$$. Consequently, even numerical investigations are nontrivial.

However, it turns out that there exist sufficient conditions! The first such conditions were stated by Wang and Xu ([2006](https://doi.org/10.1016/j.ejc.2005.05.004 "Persistent link using digital object identifier")), with important refinements by Wang ([2014](https://arxiv.org/abs/1410.2164)). These conditions are expressed using the *walk matrix* $$W\in\mathbb{Z}^{n\times n}$$ of the graph. That is, the square matrix whose columns are iterative applications of the adjacency matrix $$A$$ to the all-ones vector $$e$$:

$$
W=\bigl[e,Ae,A^2e,A^3e,\ldots,A^{n-1}e\bigr].
$$

Recall that an integer $$D\in\mathbb{Z}$$ is said to be *square-free* if it is not divisible by any nontrivial square. That is, $$p^2\nmid D$$ for all primes $$p$$. The following sufficient condition is a modification of the one by Wang. A simplified self-contained proof can be found in [arXiv:2511.19625](https://arxiv.org/abs/2511.19625).

**Theorem 4.** *Consider an undirected graph $$G$$, possibly with loops. Assume that $$\det(W)$$ is square-free. Then $$G$$ is determined by its generalized spectrum.*

While Theorem 4 also allows simple graphs, it is vacuous then. It can be shown that $$2^{\lfloor n/2\rfloor}$$ always divides the determinant of the walk matrix for a simple graph. The results by Wang ([2014](https://arxiv.org/abs/1410.2164)) also account for the special behavior of the prime $$2$$ in simple graphs. However, the setting of graphs with loops will be slightly simpler for the features that I want to discuss in this blog post. (We will likely return to the prime $$2$$ and simple graphs in future posts.)

**Example 5.** A graph with loops and associated matrices is displayed below. Note that the $$ij$$-th entry of the walk matrix counts walks of length $$j-1$$ starting at vertex $$i$$, explaining the terminology. Here, $$\det(W)=-3$$. Thus, the graph is characterized by its generalized spectrum due to Theorem 4. (Figure courtesy of [arXiv:2511.19625](https://arxiv.org/abs/2511.19625).)

![A graph with loops, its adjacency matrix, and its walk matrix](/assets/images/ExampleLoopyGraphAdjacencyWalk.png){: style="width: 100%; max-width: 800px;" .align-center}

The proof of Theorem 4 starts from the insight by Johnson and Newman that generalized cospectrality can always be realized by an orthogonal matrix that preserves the all-ones vector; recall Theorem 2.

Suppose that we are given two generalized cospectral graphs $$G$$ and $$H$$, and let $$Q\in\mathbb{R}^{n\times n}$$ be an orthogonal matrix satisfying $$Qe=e$$ and $$QA_GQ^T=A_H$$. Under mild conditions, we can prove that this matrix in fact even has rational entries:

**Lemma 6.** *Assume that $$\det(W_G)\neq 0$$. Then $$Q\in\mathbb{Q}^{n\times n}$$.*

**Proof.** By using that $$Qe=e$$ and repeatedly using that $$QA_G=A_HQ$$, we have that

$$
QW_G=W_H.
$$

Hence, $$Q=W_HW_G^{-1}$$. This is indeed a rational matrix. $$\square$$

**Definition 7.** The *level* $$\ell\in\mathbb{Z}$$ of a rational orthogonal matrix $$Q\in\mathbb{Q}^{n\times n}$$ measures the size of its denominator. That is,

$$
\ell:=\min\{L\in\mathbb{Z}_{\geq 1}:LQ\in\mathbb{Z}^{n\times n}\}.
$$

It holds that $$\ell=1$$ if and only if $$Q$$ is a signed permutation. The main goal of the argument correspondingly becomes to bound $$\ell$$. It follows from the proof of Lemma 6 and the adjugate formula for $$W_G^{-1}$$ that $$\ell\mid\det(W_G)$$. The main content in the proof of Theorem 4 is an argument that $$p\mid\ell$$ implies not only that $$p\mid\det(W_G)$$ but even $$p^2\mid\det(W_G)$$. We refer to [arXiv:2511.19625](https://arxiv.org/abs/2511.19625) for the details.

Many variants on the sufficient conditions are now known. It will be relevant in the next post that recent work has put some emphasis on the column span of $$\ell Q$$:

$$
\operatorname{Im}_{\mathbb{Z}}(\ell Q)
:=\{\ell Qv:v\in\mathbb{Z}^n\}.
$$

If $$Q\in\mathbb{Q}^{n\times n}$$ is a rational orthogonal matrix with $$Q^TAQ\in\mathbb{Z}^{n\times n}$$, then this space has the following properties:

1. It is *isotropic modulo* $$\ell^2$$. That is, $$v^Tw\equiv 0\bmod\ell^2$$ for every $$v,w\in\operatorname{Im}_{\mathbb{Z}}(\ell Q)$$.

2. It is *invariant under* $$A$$. That is, for every $$v\in\operatorname{Im}_{\mathbb{Z}}(\ell Q)$$, we also have $$Av\in\operatorname{Im}_{\mathbb{Z}}(\ell Q)$$.

3. If moreover $$Qe=e$$, then the space is orthogonal to $$e$$ modulo $$\ell$$. That is, $$e^Tv\equiv 0\bmod\ell$$ for every $$v\in\operatorname{Im}_{\mathbb{Z}}(\ell Q)$$.

The importance of these properties was emphasized in work on sufficient conditions by Guo, Wang, and Wang ([2025](https://arxiv.org/abs/2504.12932)), and in search algorithms for cospectral mates in my own work ([2026](https://arxiv.org/abs/2608.12410)).

Also relevant for our story is that Qiu, Wang, Wang, and Zhang ([2023](https://doi.org/10.1016/j.disc.2022.113177)) emphasized the importance of the *Smith normal form*. For an integer matrix $$M\in\mathbb{Z}^{n\times n}$$, there exist invertible $$U,V\in\operatorname{GL}_n(\mathbb{Z})$$ and a diagonal matrix $$D=\operatorname{diag}(d_1,\ldots,d_n)$$ such that

$$
M=UDV.
$$

The matrix $$D$$ is unique when the diagonal entries are required to be nonnegative and to satisfy $$d_1\mid d_2\mid\cdots\mid d_n$$. Note that $$\det(M)=\pm\prod_i d_i$$. The Smith normal form hence recovers the determinant up to sign. Qiu, Wang, Wang, and Zhang used the refined numerical data to prove bounds on the level when Theorem 4 is not applicable.

## Probabilistic theory using random algebraic objects

The sufficient condition in Theorem 4 implies that the frequency of generalized cospectrality could in principle be studied through number-theoretic statistics such as the determinant of the walk matrix.

O’Rourke and Touri ([2015](https://arxiv.org/abs/1511.05080)) proved that $$\det(W)$$ is nonzero with high probability in large random graphs, a result with independent interest in control theory. But how often is $$\det(W)$$ a square-free integer? To understand such questions, it turns out to be powerful to rephrase them in terms of abstract-algebraic objects.

Given a commutative ring $$R$$ and a matrix $$M\in R^{n\times n}$$, we define the *cokernel* as the finitely generated $$R$$-module that measures to what extent the induced $$R$$-linear map $$M:R^n\to R^n$$ fails to be surjective:

$$
\operatorname{coker}(M):=R^n/\operatorname{Im}_R(M),
\qquad
\operatorname{Im}_R(M):=\{Mv:v\in R^n\}.
$$

The special case $$R=\mathbb{Z}$$ will suffice for the initial discussion. Then $$\operatorname{coker}(M)$$ is simply a finitely generated Abelian group.

Studying cokernels over $$\mathbb{Z}$$ is equivalent to studying the Smith normal form. Indeed, if $$M=UDV$$ for $$U,V\in\operatorname{GL}_n(\mathbb{Z})$$ and $$D=\operatorname{diag}(d_1,\ldots,d_n)$$, then

$$
\operatorname{coker}(M)
\cong\bigoplus_{i=1}^n\mathbb{Z}/d_i\mathbb{Z}.
$$

In particular, recalling that the Smith normal form recovers the determinant up to sign, the cokernel can be used to study the square-freeness of determinants.

**Lemma 8.** *It holds that $$p^2\nmid\det(M)$$ if and only if $$\operatorname{coker}(M)\otimes_{\mathbb{Z}}(\mathbb{Z}/p^2\mathbb{Z})$$ is isomorphic to either $$0$$ or $$\mathbb{Z}/p\mathbb{Z}$$.*

At first sight, it may appear that this algebraic rephrasing makes the question more difficult, but it turns out that there are techniques that help in studying random abstract-algebraic objects associated to random matrices.[^1] To my knowledge, the first time that this connection was proposed as an approach to cospectrality problems was in my own work ([2024](https://arxiv.org/abs/2401.12655)). The ideas involved are discussed in the following sections.

### Toy case: walk matrices of digraphs with multiple edges

Let us start by considering the adjacency matrix of a random digraph that may have multiple edges. That is, we consider a random integer matrix that need not be symmetric. We denote this matrix by $$M\in\mathbb{Z}^{n\times n}$$ to disambiguate it from the (symmetric) adjacency matrix of an undirected graph.

While Theorem 4 is specific to undirected graphs, the definition of the walk matrix still makes sense for digraphs:

$$
W_M=\bigl[e,Me,M^2e,\ldots,M^{n-1}e\bigr].
$$

The digraph setting serves as a toy case. It is simpler for probabilistic purposes because the entries of the matrix $$M$$ can be taken to be independent: there is no symmetry constraint. This will allow us to explore some key ideas with fewer technicalities.

If we take the entries of $$M$$ to be fairly uniform on $$\mathbb{Z}$$, then one can study the columns of $$W_M$$ as a stochastic process. More or less, the next column is always found from the previous one by the uniform random action of $$M$$. (There are some dependencies in the process that must be accounted for, but these can be understood.) This approach can be used to prove the following:

**Theorem 9. (V.W., [2024](https://arxiv.org/abs/2401.12655))** *Fix a prime $$p$$ and an integer $$m\geq 1$$. Let $$M$$ be a $$\mathbb{Z}^{n\times n}$$-valued random matrix whose entries are independent and have the property that their reduction modulo $$p^m$$ is uniform on $$\{0,1,\ldots,p^m-1\}$$.*

*Then, for every $$k\geq 1$$ and $$0=\lambda_0\leq\lambda_1\leq\cdots\leq\lambda_k\leq m$$, it holds that, as Abelian groups,*

$$
\begin{aligned}
&\lim_{n\to\infty}
\mathbb{P}\biggl(
\operatorname{coker}(W_M)
\otimes_{\mathbb{Z}}
\frac{\mathbb{Z}}{p^m\mathbb{Z}}
\cong
\bigoplus_{i=1}^k
\frac{\mathbb{Z}}{p^{\lambda_i}\mathbb{Z}}
\biggr)
\\
&\qquad=
\prod_{i=i_0}^{\infty}\bigl(1-p^{-(i+1)}\bigr)
\prod_{j=1}^k p^{-j\delta_j},
\end{aligned}
$$

*where*

$$
i_0:=\#\{i\leq k:\lambda_i=m\},
\qquad
\delta_j:=\lambda_{k-j+1}-\lambda_{k-j}.
$$

It seems natural that the combination of Lemma 8 and Theorem 9 should yield the probability that $$\det(W_M)$$ is square-free for a random matrix $$M$$ whose entries are uniform on $$[-m,m]\cap\mathbb{Z}$$ as $$m\to\infty$$. However, some care is required. There will always be some primes $$p$$ with $$p^2\gg m$$. The entries of $$M$$ are then far from uniform modulo $$p^2$$, so Theorem 9 cannot be directly used. This motivates the following:

**Definition 10.** A collection of $$\mathbb{Z}$$-valued random variables $$\{D_i:i\in\mathcal{I}\}$$ satisfies a *large primes estimate for square-freeness* if for every $$\varepsilon>0$$ there exists $$C>0$$ with

$$
\sup_{i\in\mathcal{I}}
\mathbb{P}\bigl(\exists p>C:p^2\mid D_i\bigr)
\leq\varepsilon,
$$

where $$p$$ runs over prime numbers.

**Corollary 11. (Square-freeness conditional on large primes)** *For every $$m,n\geq 1$$, let $$M=M(n,m)$$ be a random $$n\times n$$ matrix with independent entries uniform from $$[-m,m]\cap\mathbb{Z}$$.*

*Assume that $$\{\det(W_{M(n,m)}):n,m\geq 1\}$$ is known to satisfy a large primes estimate for square-freeness. Then*

$$
\begin{aligned}
&\lim_{n\to\infty}\lim_{m\to\infty}
\mathbb{P}\bigl(\det(W_M)\textnormal{ is square-free}\bigr)
\\
&\qquad=
\prod_p
\Bigl((1+p^{-1})\prod_{i=0}^{\infty}(1-p^{-i-1})\Bigr).
\end{aligned}
$$

**Proof.** Note that the events that $$p^2\mid\det(W_M)$$ are asymptotically independent over every fixed finite set of primes $$p$$ as $$m\to\infty$$. The result hence follows from Lemma 8 by using Theorem 9 to estimate the probability that $$\operatorname{coker}(W_M)\otimes(\mathbb{Z}/p^2\mathbb{Z})$$ is isomorphic to either $$0$$ or $$\mathbb{Z}/p\mathbb{Z}$$. $$\square$$

So, square-freeness of determinants can be reduced to studying the $$p$$-parts of the cokernel *conditional on a large primes estimate*. (What can be proved concerning large prime estimates is discussed later.) That is, at least for the very special distribution with all entries completely independent and uniform on a large set.

### Exploiting $$\mathbb{Z}[x]$$-module structure

What can be said about different random matrix ensembles? The technique that is used to prove Theorem 9 by studying the columns as a stochastic process relies heavily on the uniformity and independence of the entries. It is not so easy to extend this method to different settings. To this end, it turns out to be helpful to use that $$\operatorname{coker}(W_M)$$ is equipped with richer algebraic structure than just a group.

A matrix $$M\in\mathbb{Z}^{n\times n}$$ induces a $$\mathbb{Z}[x]$$-module structure on $$\mathbb{Z}^n$$ defined by $$xv=Mv$$ for $$v\in\mathbb{Z}^n$$. With this definition, the image of the walk matrix is exactly the $$\mathbb{Z}[x]$$-module span of the all-ones vector:

$$
\operatorname{Im}_{\mathbb{Z}}(W_M)
=
\operatorname{span}_{\mathbb{Z}}(M^ie:i\geq 0)
=
\mathbb{Z}[x]e.
$$

Thus, the quotient $$\operatorname{coker}(W_M)=\mathbb{Z}^n/(\mathbb{Z}[x]e)$$ is also naturally a $$\mathbb{Z}[x]$$-module.

This module structure is useful when extending results to different models. The precise statement is somewhat technical, but it can be simplified subject to a different type of large primes assumption. The ring $$\mathbb{Z}[x]$$ is two-dimensional and has maximal ideals of the form $$\mathfrak{m}=p\mathbb{Z}[x]+\beta(x)\mathbb{Z}[x]$$ with $$p$$ a prime and $$\beta(x)\in\mathbb{Z}[x]$$ a polynomial with irreducible reduction in $$\mathbb{F}_p[x]$$. There are hence “two directions” for the maximal ideals: the prime direction $$p$$ and the polynomial direction $$\beta(x)$$.

The following terminology is not standard, but it is clarifying for our purposes:

**Definition 12.** Fix a prime $$p$$. For every $$d\geq 1$$, denote

$$
\mathcal{B}(p,d):=
\{\beta\in\mathbb{F}_p[x]:
\beta\textnormal{ is irreducible and }\deg(\beta)\geq d\}.
$$

Then a collection of random $$\mathbb{Z}[x]$$-modules $$\{M_i:i\in\mathcal{I}\}$$ is said to satisfy a *large polynomials estimate at* $$p$$ if for every $$\varepsilon>0$$ there exists $$d\geq 1$$ such that

$$
\sup_{i\in\mathcal{I}}
\mathbb{P}\Bigl(
\exists\beta\in\mathcal{B}(p,d):
M_i\otimes
\frac{\mathbb{F}_p[x]}{\beta\mathbb{F}_p[x]}
\neq 0
\Bigr)
<\varepsilon.
$$

With this notation, we can give a conditional universality result. (Rather, we can give an unconditional result whose statement simplifies conditional on large polynomial estimates.) One more definition is useful to clarify that the entries’ law does not matter subject to reasonable constraints, but one can think of nondegenerate $$\{0,1\}$$-valued entries as the main example of interest.

**Definition 13.** A $$\mathbb{Z}$$-valued random variable $$D$$ is said to be $$\epsilon$$-balanced if

$$
\sup_p\max_{v\in\mathbb{F}_p}
\mathbb{P}(D\equiv v\bmod p)
\leq 1-\epsilon,
$$

where $$p$$ runs over prime numbers.

**Theorem 14. (V.W., [2024](https://arxiv.org/abs/2401.12655))** *Fix some $$\epsilon>0$$. For every $$n\geq 1$$, let $$M(n)$$ be a random $$n\times n$$ integer matrix whose entries are independent and $$\epsilon$$-balanced.*

*Assume that $$\{\det(W_{M(n)}):n\geq 1\}$$ satisfies a large primes estimate for square-freeness, and moreover that $$\{\operatorname{coker}(W_{M(n)}):n\geq 1\}$$ satisfies a large polynomials estimate at every prime $$p$$. Then*

$$
\begin{aligned}
&\lim_{n\to\infty}
\mathbb{P}\bigl(\det(W_M)\textnormal{ is square-free}\bigr)
\\
&\qquad=
\prod_p
\Bigl((1+p^{-1})\prod_{i=0}^{\infty}(1-p^{-i-1})\Bigr).
\end{aligned}
$$

We stated that exploiting $$\mathbb{Z}[x]$$-module structure is essential. To clarify why, we conclude this section with a proof outline. The details of this argument are not needed in what follows in this or the following post. The outline is only given to clarify why the $$\mathbb{Z}[x]$$-module structure is so important.

**Proof outline for Theorem 14.** We rely on the *category-theoretic moment method* of Wood ([2014](https://arxiv.org/abs/1402.5149)) and Sawin–Wood ([2022](https://arxiv.org/abs/2210.06279)). In classical probability theory, the moment method refers to the fact that the distribution of an $$\mathbb{R}$$-valued random variable $$Y$$ can be deduced from its moments $$\{\mathbb{E}[Y^n]:n\geq 0\}$$ subject to mild conditions. The category-theoretic moment method implements a similar idea.

Let $$\mathcal{Y}$$ be a random algebraic object (say a group or a module). Then the role of the natural number $$n\geq 0$$ may be replaced by a fixed finite object $$N$$. The *$$N$$-th moment* of $$\mathcal{Y}$$ is then the expected number of surjective morphisms to $$N$$:

$$
m_N:=\mathbb{E}[\#\operatorname{Sur}(\mathcal{Y},N)].
$$

The results of Sawin–Wood ([2022](https://arxiv.org/abs/2210.06279)) allow one to recover the distribution of an algebraic object from its moments subject to mild assumptions. (Note: the distribution is only characterized in a *profinite* topology. This is ultimately why separate large prime and polynomial problems are also necessary.)

The moment method is a powerful way to study the distribution of cokernels of random matrices. For example, it is relatively tractable to determine the moments of the Abelian group $$\operatorname{coker}(M)$$ when $$M$$ is a random matrix with independent entries; see Wood ([2015](https://arxiv.org/abs/1504.04391)). However, the entries of our matrix $$W_M$$ are not at all independent! The columns of $$W_M$$ are nontrivial algebraic combinations of the entries of $$M$$. By instead estimating the moments in the category of $$\mathbb{Z}[x]$$-modules, we can effectively untwist these algebraic dependencies.

In particular, by pulling back the morphisms $$f:\operatorname{coker}(W_M)\to N$$ through the natural quotient map $$\mathbb{Z}^n\to\operatorname{coker}(W_M)$$, one can show that the $$\mathbb{Z}[x]$$-theoretic $$N$$-moment satisfies

$$
\begin{aligned}
&\mathbb{E}\Bigl[
\#\operatorname{Sur}_{\mathbb{Z}[x]}
\bigl(\operatorname{coker}(W_M),N\bigr)
\Bigr]
\\
&\qquad=
\sum_{\substack{
F\in\operatorname{Sur}_{\mathbb{Z}}(\mathbb{Z}^n,N)\\
F(e)=0
}}
\mathbb{P}(F\circ M=xF).
\end{aligned}
$$

Here, the sum runs over surjective group morphisms $$F:\mathbb{Z}^n\to N$$ with $$F(e)=0$$. Note that the problem has been linearized! The probability refers directly to $$M$$, not to the more complicated matrix $$W_M$$. This trick is possible for $$\mathbb{Z}[x]$$-module moments, but not for moments as Abelian groups.

One can then analyze the sum on the right-hand side to show that $$\mathbb{E}[\#\operatorname{Sur}_{\mathbb{Z}[x]}(\operatorname{coker}(W_M),N)]\approx(\#N)^{-1}$$ and use the category-theoretic moment method to conclude. We refer to [arXiv:2401.12655](https://arxiv.org/abs/2401.12655) for the details. $$\square$$

### Undirected graphs

Theorem 14 tells us the probability of square-freeness in digraphs. However, the sufficient condition in Theorem 4 is only applicable to undirected graphs. The sufficient conditions are sensitive to symmetry constraints, and numerical evidence suggests that they then apply with different frequency. Some of the key ideas developed surrounding Theorem 14, however, also turn out to be applicable in the setting of undirected graphs!

Recent work of Nikita Lvov and myself ([2026](https://arxiv.org/abs/2603.26932)) studied the satisfaction frequency of arithmetic sufficient conditions for spectral determination in random matrix models with symmetries. The perspective of $$\mathbb{Z}[x]$$-modules and cokernels is also crucial there. In particular, while a random matrix model with uniform random integer entries is analytically tractable when all entries are independent (Theorem 9), it is much less tractable if there is a symmetry constraint. It turns out, however, that an analytically tractable random matrix model could be found by taking uniform random entries from $$\mathbb{Z}[x]$$. (Or rather, the profinite completion of this ring.)

Moreover, such $$\mathbb{Z}[x]$$-theoretic perspectives are also applicable to sufficient conditions different from the walk matrix. Let us discuss one example that will be helpful to connect with the large prime problems in the following section.

Recall from Theorem 2 and Lemma 6 that, subject to the mild condition that $$\det(W)\neq 0$$, generalized cospectrality is always realized by conjugacy with a rational orthogonal matrix $$Q\in\mathbb{Q}^{n\times n}$$ satisfying $$Qe=e$$. It is natural to wonder what can be said if we only restrict the field of the entries of $$Q$$ but do not impose the constraint that $$Qe=e$$. A sufficient condition for such a notion exists:

**Theorem 15. (Wang and Yu, [2016](https://arxiv.org/abs/1608.01144))** *Let $$A\in\mathbb{Z}^{n\times n}$$ be a symmetric integer matrix with eigenvalues $$\lambda_1\leq\cdots\leq\lambda_n$$. Then*

$$
\Delta_A:=\prod_i\prod_{j\neq i}(\lambda_i-\lambda_j)
$$

*is an integer. Moreover, if $$\Delta_A$$ is odd and square-free, then the only rational orthogonal matrices $$Q\in\mathbb{Q}^{n\times n}$$ with $$Q^TAQ\in\mathbb{Z}^{n\times n}$$ are in fact signed permutations.*

An alternative proof and generalizations to orthogonal matrices with entries in an arbitrary fixed number field can be found in my recent [2026](https://arxiv.org/abs/2608.12410) work.

As it turns out, the $$\mathbb{Z}[x]$$-module structure of the cokernel of the matrix $$A-xI\in\mathbb{Z}[x]^{n\times n}$$ can be used to analyze conditions based on the walk matrix and conditions based on $$\Delta_A$$. For example:

**Conjecture 16. (Lvov, V.W., [2026](https://arxiv.org/abs/2603.26932))** *Suppose that $$A$$ is chosen uniformly at random from all symmetric $$n\times n$$ matrices with $$\{0,1\}$$-valued entries. Then, for every prime $$p$$,*

$$
\lim_{n\to\infty}\mathbb{P}(p\nmid\Delta_A)
=
\Bigl(1-\frac{1}{p}\Bigr)
\prod_{k=1}^{\infty}
\Bigl(1-\frac{1}{p^{2k}}\Bigr).
$$

*Further, for every odd prime $$p$$,*

$$
\lim_{n\to\infty}\mathbb{P}\bigl(p^2\nmid\Delta_A\bigr)
=
\Bigl(1-\frac{1}{p^2}\frac{3p-1}{p+1}\Bigr)
\prod_{k=1}^{\infty}
\Bigl(1-\frac{1}{p^{2k}}\Bigr).
$$

This conjecture was deduced by proving a variant of it in a different analytically tractable random matrix model. To actually deduce rigorous bounds on the probability of square-freeness, one would consequently also need universality results like Theorem 14 and large prime estimates.

## Large prime estimates

Recall our definition of large prime estimates from Definition 10. The fact that such estimates are a key technical problem in square-freeness estimates is classical in arithmetic statistics, the area of number theory concerned with probabilistic results.

Given an integer polynomial $$f\in\mathbb{Z}[x_1,\ldots,x_n]$$, large prime estimates on $$f(X_1,\ldots,X_n)$$ for $$X_i\sim\operatorname{Unif}\{-m,\ldots,m\}$$ are a classical challenging topic; see, for example, Hooley ([1967](https://doi.org/10.1112/S002557930000797X)), Nair ([1976](https://doi.org/10.1112/S0025579300008779)), and Heath-Brown ([2011](https://arxiv.org/abs/1103.2028)). For a general irreducible polynomial $$f$$, unconditional results are unfortunately only available in low degree. Extending the range of unconditional results for monic polynomials to degree $$d\leq 8$$ was one of the results claimed by OpenAI in their preprint dump on October 6 ([2026](https://github.com/openai/math/blob/main/preprints/Squarefree-values-of-quartics-and-power-free-values-of-polynomials-September-24-2026/manuscript.pdf)).

Granville ([1998](https://doi.org/10.1155/S1073792898000592)) provides estimates for monic polynomials of arbitrary degree conditional on the *abc*-conjecture. Poonen ([2002](https://arxiv.org/abs/math/0203292)) also gives estimates conditional on *abc* for multivariate polynomials in a slightly modified measure where one of the variables is much larger than the others. These multivariate results can be applied to $$\det(W_M)$$ and $$\Delta_M$$ when $$M$$ has random integer entries, but only for conditional results.

Our statistics of interest are, however, not arbitrary polynomials in the entries of $$M$$. They have natural interactions with the matrix structure that one may hope to exploit. This has not yet been pursued in the special case of $$\det(W_M)$$ and $$\Delta_M$$, but some closely related problems have been investigated.

The most relevant results are probably those of Nguyen and Wood ([2018](https://arxiv.org/abs/1806.00596), [2022](https://arxiv.org/abs/2210.08526)). They studied the probability that the cokernel $$\operatorname{coker}(M)$$ of a random matrix is a cyclic group. That is, a group of the form $$\mathbb{Z}/n\mathbb{Z}$$.

**Theorem 17. (Nguyen and Wood, [2022](https://arxiv.org/abs/2210.08526))** *Let $$M$$ be a random symmetric $$n\times n$$ matrix whose upper-triangular entries $$\{M_{i,j}:i\leq j\}$$ are i.i.d. copies of an integer-valued $$\epsilon$$-balanced random variable. Then*

$$
\lim_{n\to\infty}
\mathbb{P}\bigl(\operatorname{coker}(M)\textnormal{ is cyclic}\bigr)
=
\prod_{i=1}^{\infty}\zeta(2i+1)^{-1}
\approx 0.7935\ldots
$$

*Here, $$\zeta$$ is the Riemann zeta function.*

Unlike most problems considered in previous works on cokernel statistics, this is a “global” problem insofar as it depends on all primes simultaneously. Indeed, a finite Abelian group $$G$$ is cyclic if and only if $$G\otimes\mathbb{Z}/p\mathbb{Z}$$ is cyclic for *every* prime $$p$$.

The proof by Nguyen and Wood separated the problem into estimates for small primes, where cyclicity sometimes fails, and estimates for large primes, where cyclicity ultimately does not fail. While the large primes are ultimately insubstantial, proving this is a different story! The large prime estimates in the proof of Theorem 17 are highly nontrivial and subdivide the largeness into various ranges.

Note that $$\operatorname{coker}(M)$$ being cyclic is a necessary condition for $$\det(M)$$ to be square-free. Indeed, recall that the Smith normal form allows us to write $$\operatorname{coker}(M)\cong\bigoplus_i\mathbb{Z}/d_i\mathbb{Z}$$ for unique nonnegative integers $$d_1\mid d_2\mid\cdots\mid d_n$$ and that $$\det(M)=\pm\prod_i d_i$$. If $$d_{n-1}\neq 1$$, then $$\det(M)$$ is not square-free. The cokernel being cyclic is, however, *not* a sufficient condition for $$\det(M)$$ to be square-free.

For example, it is possible to have $$p^2\mid\det(M)$$ if the first $$n-1$$ columns of $$M$$ have rank $$n-1$$ over $$\mathbb{F}_p$$ but the final column is divisible by $$p^2$$. A crucial proof-technical difference between cyclicity and square-freeness is that cyclicity can be seen from only “mod $$p$$ considerations”, while square-freeness also requires “mod $$p^2$$ considerations”. It is known among experts that ruling out “mod $$p^2$$ considerations” is extremely difficult. To my knowledge, square-freeness results for $$\det(M)$$ in the setting of Theorem 17 are hence not currently known.

One of the only related cases where such issues have been successfully ruled out is in a breakthrough paper by Bhargava, Shankar, and Wang ([2016](https://arxiv.org/abs/1611.09806)) that studied the probability of square-freeness for the discriminant $$\Delta_f=\prod_i\prod_{j\neq i}(\lambda_i-\lambda_j)$$ of a random monic integer polynomial $$f\in\mathbb{Z}[x]$$ with independent coefficients. (Here, the $$\lambda_i$$ are the roots of $$f$$.) It is possible to have $$p^2\mid\Delta_f$$ for “mod $$p$$ considerations” that only depend on $$f\bmod p$$ or for “mod $$p^2$$ considerations” that really require the information in $$f\bmod p^2$$. The result by Bhargava, Shankar, and Wang also had a method to rule out “mod $$p^2$$ considerations” for large primes.

## Boosting the probability using fixed-level estimates

Even if one could rigorously prove some version of Conjecture 16 or related conjectures, this in isolation would only show that a nonvanishing fraction of graphs is determined by its generalized spectrum. We know that $$\det(W)$$ and $$\Delta_A$$ will *not* be square-free with probability one. The best that we can hope to establish is a nonvanishing bound on the probability, showing that it is strictly between zero and one.

However, recall that prime divisors of the level $$p\mid\ell$$ are square prime divisors of the determinant $$p^2\mid\det(W)$$, and also that $$\ell\mid\det(W)$$. This implies that if the determinant has prime factorization $$\det(W)=\pm \prod_i p_i^{e_i}$$, then

$$
\ell\leq\prod_{i:e_i\geq 2}p_i^{e_i}.
$$

If one could establish that $$\det(W)$$ was square-free with nontrivial probability, then the same methods would likely be able to show that the prime factorization $$\det(W)=\pm\prod_i p_i^{e_i}$$ has only a few exponents $$e_i\geq 2$$ and that these are all for small primes.

Thus, the following conjecture should not be more difficult than the preceding ones:

**Conjecture 18. (Small levels)** Let $$A$$ be the adjacency matrix of a random graph on $$n$$ vertices. Let $$\ell\geq 1$$ be the greatest level of a rational orthogonal matrix $$Q\in\mathbb{Q}^{n\times n}$$ with $$Qe=e$$ such that $$Q^TAQ\in\mathbb{Z}^{n\times n}$$. Then, for every $$\varepsilon>0$$, there exists some $$C>0$$ such that $$\limsup_{n\to\infty}\mathbb{P}(\ell>C)\leq\varepsilon$$.

The following result of Wang and Zhao ([2025](https://arxiv.org/abs/2509.05781)), however, rules out small levels:

**Theorem 19. (Wang and Zhao, [2025](https://arxiv.org/abs/2509.05781))** Fix some $$\ell\geq 2$$. Let $$G$$ be a random graph on $$n$$ vertices. Then

$$
\begin{aligned}
\lim_{n\to\infty}
\mathbb{P}\bigl(
& G\textnormal{ has a generalized cospectral mate}\\
& \textnormal{with level }\ell
\bigr)
=0.
\end{aligned}
$$

The proof by Wang and Zhao involves a union bound over all rational orthogonal matrices with a given level.

Conditional on Conjecture 18, one could use Theorem 19 to prove that almost all graphs are determined by their generalized spectrum. Thus, one could boost the probability from nonvanishing to one.

## Conclusion: an outline of a strategy

The following general strategy for proving bounds on the probability of generalized cospectrality becomes apparent from the preceding discussion:

1. Consider some deterministic sufficient condition.
2. Rephrase the sufficient condition in terms of abstract-algebraic objects associated to a random matrix.
3. Study the distribution of the local pieces of the algebraic objects that lie over small primes.
4. Rule out the contribution of the pieces of the algebraic objects that lie over large primes.

This general strategy had been identified in previous works. (See, for example, Sections 1.2 and 1.3 in a [2026](https://arxiv.org/abs/2603.26932) preprint by Nikita and myself.) However, the precise implementation of such a strategy remained a nontrivial open problem. For example, it should be clear that large prime problems remained highly challenging.

So, what methods were actually used in the preprint [“Almost all graphs are determined by their generalized spectrum”](https://arxiv.org/abs/2610.11047)? This is discussed in the next post. We will see that the high-level scheme of the proof follows the strategy outlined above, but that some new approaches were used to circumvent key bottlenecks.

[^1]: Algebraic objects associated to random matrices also occur in the study of sandpiles on random graphs, in homology groups for topological data analysis, and in connection to the Cohen–Lenstra heuristics in algebraic number theory. See Clancy, Kaplan, Leake, Payne, and Wood ([2014](https://arxiv.org/abs/1402.5129)) for sandpile groups, Kahle, Lutz, Newman, and Parson ([2017](https://arxiv.org/abs/1710.05683)) for homology groups, and Wood ([2015](https://arxiv.org/abs/1504.04391)) for the Cohen–Lenstra conjectures. Readers who think that this sounds very exciting may be interested to know that a new online seminar on such topics is being organized by Nikita Lvov and myself: the [Probability and Algebra Seminar](https://sites.google.com/view/probability-algebra-seminar/).
