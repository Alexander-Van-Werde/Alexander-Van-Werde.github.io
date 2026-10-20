---
layout: single
title: "Initial impressions - Previous work"
date: 2026-10-20 12:05:00 +0200
tags:
  - Initial-Impressions
author: alexander
---
**Author:** {{ site.data.authors[page.author].name }}

 
Before we can appreciate what ideas are new in the preprint, we need to understand the context of previous work. This is the goal of this second post. I will also use this opportunity to tell a cohesive story with a few outlines of key proofs ideas in the literature. This may be of independent interest, as a similar review of the subject is not previously available. 

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

The term _graph_ is reserved in this post are to finite and undirected graphs. Directed graphs will be explicitly be referred to as digraphs. 

We do _not_ assume that the graphs are simple. Self loops and multiple edges are permissible. Let me warn that many of the references that I'll mention are stated for simple graphs. The key points for my story however extend to the general setting, and the flexibility of allowing loops will be useful in some places. 

**Definition 1.**  Two graphs 𝐺 and 𝐻 are _generalized cospectral_ if their adjacency matrices have the same characteristic polynomial, and their complement graphs also have the same characteristic polynomial. We say that $G$ is _determined by its generalized spectrum (DGS)_ if all generalized cospectral graphs $H$ are in-fact isomorphic to $G$. 

This notion dates back to Johnson and Newman ([1980](https://doi.org/10.1016/0095-8956(80)90058-1)) who arrived at it from a different direction. Their paper started from the perspective that the choice to take entries $0$ and $1$ in the usual adjacency matrix was somewhat arbitrary, and investigated what happens if one uses formal symbols $x$ and $y$ instead. They proved that the $xy$-adjacency matrices $A^{x,y}_G$ and $A_H^{x,y}$ have the same spectrum for every choice of $x,y\in  \mathbb{R}$ if and only if the graphs are generalized cospectral! 

Johnson and Newman also proved different equivalent formulations. One of these is relevant for our story. Let $e= (1,\ldots,1)^T$ be the all-ones vector, with the dimension matching the number of vertices $n$ in $G$.

**Theorem 2. (Johnson and Newman, 1980)** _Two graphs $G$ and $H$ have the same generalized spectrum if and only if there exists an orthogonal matrix $Q\in \mathbb{R}^{n\times n}$ satisfying  $Q e = e$ that relates their adjacency matrices by conjugacy $Q A_G Q^T = A_H$._ 

It is not difficult to check that the existence of such an orthogonal matrix implies generalized cospectrality.  The opposite direction requires an argument, omitted here for brevity. 

**Remark 3.** The role of the all-ones vector is partly for aesthetic reasons. Up to scalar multiplication, it is the only non-trivial vector that is canonically defined. Given a different integer vector $\xi\in \mathbb{Z}^n$ one can also define a notion of cospectrality for the bivariate characteristic polynomial  $\Phi_G \in \mathbb{Z}[\lambda, t]$ defined by $\Phi_G = \det(\lambda I - A_G + t \xi \xi^T)$.   Much of the theory can be extended to this setting if one replaces the all-ones vector by $\xi$.  Details and references can be found in [arXiv:2511.19625](https://arxiv.org/abs/2511.19625). 

## Deterministic sufficient conditions 

While it is clear that generalized cospectrality is more restrictive than ordinary cospectrality, it is not clear how specifically this additional information would make it easier to prove that a given graph is determined by its generalized spectrum. The equivalent definitions of Johnson and Newman still all make reference to the candidate cospectral graph. Hence, to show that $G$ is determined by its generalized spectrum one has to enumerate all other potential graphs $H$. Consequently, even numerical investigations are nontrivial.

However, it turns out that there exist sufficient conditions! The first such conditions were stated by Wang and Xu ([2006](https://doi.org/10.1016/j.ejc.2005.05.004 "Persistent link using digital object identifier")) with important refinements by Wang ([2014](https://arxiv.org/abs/1410.2164)). These conditions are expressed using the walk matrix _walk matrix $W\in \mathbb{Z}^{n\times n}$_ of the graph. That is, the square matrix whose columns are iterative applications of the adjacency matrix $A$ to the all-ones vector $e$:  
$$W = \bigl[e, Ae, A^2 e, A^3 e, \ldots, A^{n-1}e\bigr] $$


Recall that an integer $D\in \mathbb{Z}$ is said to be _square-free_ if it is not divisible by any non-trivial square. That is, $p^2\nmid D$ for all primes $p$. The following sufficient condition is a modification of the one by Wang. A simplified self-contained proof can be found in ([arXiv:2511.19625](https://arxiv.org/abs/2511.19625)).  

**Theorem 4.** _Consider an undirected graph $G$, possibly with loops.  Assume that $\det(W)$ is square-free. Then, $G$ is determined by its generalized spectrum._

While Theorem 4 also allows simple graphs, it is vacuous then. It can be shown that $2^{\lfloor n/2 \rfloor}$ always divides the determinant of the walk matrix for a simple graph. The results by Wang ([2014](https://arxiv.org/abs/1410.2164)) also account for the special behavior of the prime $2$ in simple graphs. However, the setting of graphs with loops will be slightly simpler for the features that I want to discuss in this blog post. (We will likely return to the prime $2$ and simple graphs in future posts.) 

**Example 5.** A graph with loops and associated matrices is displayed below. Note that the $ij$-th entry of the walk matrix counts walks of length $j-1$ starting at vertex $i$, explaining the terminology. It here holds that $\det(W) = -3$. Thus, the graph is characterized by its generalized spectrum due to Theorem 4.  (Figure courtesy of [arXiv:2511.19625](https://arxiv.org/abs/2511.19625))

![](/assets/images/ExampleLoopyGraphAdjacencyWalk.png){: style="width: 100%; max-width: 800px;" .align-center}

   

The proof of Theorem 4 starts from the insight by Johnson and Newman that generalized cospectrality can always be realized by an orthogonal matrix that preserves the all-ones vector; recall Theorem 2. 

Suppose that we are given two generalized cospectral graphs $G$ and $H$ and let $Q\in \mathbb{R}^{n\times n}$ be an orthogonal matrix satisfying $Qe = e$ and $Q A_G Q^T = A_H$. Under mild conditions, we can prove that this matrix in-fact even has rational entries:

**Lemma 6.** _Assume that $\det(W_G) \neq 0$. Then, $Q\in \mathbb{Q}^{n\times n}$._

**Proof.** By using that $Qe = e$ and repeatedly using that $QA_G = A_HQ$ we have that 
$$Q W_G = W_H.$$
Hence, $Q = W_{H} W_{G}^{-1}$. This is indeed a rational matrix. $\qed$ 

**Definition 7.** The _level_ $\ell\in \mathbb{Z}$ of a rational orthogonal matrix $Q\in \mathbb{Q}^{n\times n}$ measures the size of its denominator. That is, $\ell := \min\{L\in \mathbb{Z}_{\geq 1}: L Q \in \mathbb{Z}^{n\times n}   \}.$

It holds that $\ell = 1$ if and only if $Q$ is a signed permutation. The main goal of the argument correspondingly becomes to bound $\ell$. It follows from the proof of Lemma 6 and the adjoint formula for $W_G^{-1}$ that $\ell\mid \det(W_G)$. The main content in the proof of Theorem 4 is an argument that in-fact $p\mid \ell$ implies not only that $p\mid \det(W_G)$ but even $p^2 \mid \det(W_G)$. We refer to [arXiv:2511.19625](https://arxiv.org/abs/2511.19625) for the details.

Many variants on the sufficient conditions are now known. It will be relevant in the next post that recent work has put some emphasis on the column span of $\ell Q$:
$$\operatorname{Im}_\mathbb{Z}(\ell Q) := \{ \ell Q v: v\in \mathbb{Z}^n  \}.$$
If $Q\in \mathbb{Q}^{n\times n}$ is a rational orthogonal matrix with $Q^T A Q\in \mathbb{Z}^{n\times n}$ then this space has the following properties: 
1. It is _isotropic mod $\ell^2$_. That is, it holds that $v^T w \equiv 0 \bmod \ell^2$ for every $v,w\in \operatorname{Im}_{\mathbb{Z}}(\ell Q)$. 
2. It is $A$-invariant. That is, it holds for every $v\in \operatorname{Im}_{\mathbb{Z}}(\ell Q)$ that also $Av\in \operatorname{Im}_{\mathbb{Z}}(\ell Q)$.
If moreover $Qe = e$, then the space has the following property:
3. It is orthogonal to $e$ modulo $\ell$. That is, $e^T v \equiv 0\bmod \ell$ for every $v\in \operatorname{Im}_{\mathbb{Z}}(\ell Q)$.    
The importance of these properties was emphasized in work on sufficient conditions by Guo, Wang, and Wang ([2025](https://arxiv.org/abs/2504.12932)), and in search algorithms for cospectral mates in my own work ([2026](https://arxiv.org/abs/2608.12410)).     

Also relevant for our story is that Qiu, Wang, Wang, and Zhang ([2023](https://doi.org/10.1016/j.disc.2022.113177)) emphasized the importance of the _Smith normal form_. For an integer matrix $M\in \mathbb{Z}^{n\times n}$, there exist invertible $U,V \in \operatorname{GL}_n(\mathbb{Z})$ and a diagonal matrix $D = \operatorname{diag}(d_1,\ldots,d_n)$ such that 
$$M = U D V.$$
The matrix $D$ is unique subject to the constraint that $d_1 \mid d_2 \mid \cdots \mid d_n$.  Note that $\det(M) = \pm \prod_i d_i$. The Smith normal form hence recovers the determinant up to sign. Qiu, Wang, Wang, and Zhang used the refined numerical data to prove bounds on the level when Theorem 4 is not applicable.  

##  Probabilistic theory using random algebraic objects

The sufficient condition in Theorem 4 implies that the frequency of generalized cospectrality could in-principle be studied through number-theoretic statistics such as the determinant of the walk matrix.  

O’Rourke and Touri ([2015](https://arxiv.org/abs/1511.05080)) proved that $\det(W)$ is non-zero with high probability in large random graphs, a result with independent interest in control theory.  But, how often is $\det(W)$ a square-free integer?  To understand such questions, it turns out to be powerful to rephrase in terms of abstract-algebraic objects.  

Given a commutative ring $R$ and a matrix $M\in R^{n\times n}$, we define the _cokernel_ as the finitely generated $R$-module that measures to what extent the induced $R$-linear map $M:R^n \to R^n$ fails to be surjective: 
$$\operatorname{coker}(M) := R^n/\operatorname{Im}_R(M)\ \textnormal{ where }\ \operatorname{Im}_R(M) := \{Mv: v\in R^n \}.$$
The special case $R=\mathbb{Z}$ will suffice for the initial discussion. Then, $\operatorname{coker}(M)$ is simply a finitely generated Abelian group. 

Studying cokernels over $\mathbb{Z}$ is equivalent to studying the Smith normal form. Indeed, if $M=UDV$ for $U,V\in \operatorname{GL}_n(\mathbb{Z})$ and $D = \operatorname{diag}(d_1,\ldots,d_n)$ then $$\operatorname{coker}(M) = \oplus_{i=1}^n \mathbb{Z}/d_i \mathbb{Z}.$$In particular, recalling that the Smith normal form recovers the determinant up to sign, the cokernel can be used to study the square-freeness of determinants. 

**Lemma 8.** _It holds that $p^2 \nmid\det(M)$ if and only if_ $\operatorname{coker}(M)\otimes_{\mathbb{Z}} (\mathbb{Z}/p^2 \mathbb{Z})  \in \{0, \mathbb{Z}/p\mathbb{Z}  \}$. 

At first sight, it may appear that this algebraic rephrasing makes the question more difficult, but it turns out that there are techniques that help in studying random abstract-algebraic objects associated to random matrices.[^1] To my knowledge, the first time that this connection was proposed as an approach to cospectrality problems was in my own work ([2024](https://arxiv.org/abs/2401.12655)). The ideas involved are discussed in the following sections.

### Toy case: walk matrices of digraphs with multiple edges

Let us start by considering the adjacency matrix of a random digraph that may have multiple edges. That is, we consider a random integer matrix that need-not be symmetric. We denote this matrix by $M \in \mathbb{Z}^{n\times n}$ to disambiguate it from the (symmetric) adjacency matrix of an undirected graph. 

While Theorem 4 is specific to undirected graphs, the definition of the walk matrix still makes sense for digraphs: 
$$W_M = \bigl[e,Me,M^2e ,\ldots, M^{n-1}e\bigr] $$
The digraph setting serves as a toy case. It is simpler for probabilistic purposes because the entries of the matrix $M$ can be taken to be independent: there is no symmetry constraint.  This will allow exploring some key ideas with fewer technicalities.  

If we take the entries of $M$ to be fairly uniform on $\mathbb{Z}$ then one can study the columns of $W_M$ as a stochastic process. More or less, the next column is always found from the previous one by the uniform random action of $M$. (There are some dependencies in the process that must be accounted for, but these can be understood.) This approach can be used to prove the following: 

**Theorem 9. (V.W., [2024](https://arxiv.org/abs/2401.12655))**  _Fix a prime $p$ and an integer $m\geq 1$. Let $M$ be a $\mathbb{Z}^{n\times n}$-valued random matrix whose entries are independent have the property that the reduction $\bmod p^2$ is uniform on $\{0,1,\ldots,p^{m}-1 \}$._

_Then, it holds for every $k \geq 1$ and $0 = \lambda_0 \leq \lambda_1 \leq \cdots \leq \lambda_k$ that, as Abelian groups,_ 
$$\lim_{n\to \infty}\mathbb{P}\biggl(\operatorname{coker}(W_M) \otimes_{\mathbb{Z}}\frac{\mathbb{Z}}{p^{m}\mathbb{Z}} \cong  \bigoplus_{i=1}^k \frac{\mathbb{Z}}{p^{\lambda_i} \mathbb{Z}}  \biggr)  = \prod_{i=i_0}^\infty \bigl(1 - p^{-(i+1)}\bigr) \prod_{j=1}^k p^{-j \delta_j}$$
_where_
$$i_0 := \#\{i\leq k: \lambda_i = m \}\ \textnormal{ and }\ \delta_j := \lambda_{k-j+1} - \lambda_{k-j}.$$

It seems natural that the combination of Lemma 8 and Theorem 9 should yield the probability that $\det(W_M)$ is square-free for a random matrix $M$ whose entries are uniform on $[-m,m]\cap \mathbb{Z}$ as $m\to \infty$.   However, some care is required. There will always be some primes $p$ with $p^2 \gg m$. The entries of $M$ are then far from uniform modulo $p^2$, so Theorem 9 can not be directly used.  This motivates the following: 

**Definition 11.** A collection of $\mathbb{Z}$-valued random variables $\{D_i : i\in \cI \}$ satisfies a _large primes estimate for square-freeness_ if for every $\varepsilon>0$ there exists $C>0$ with
$$\max_{i\in \cI} \mathbb{P}\bigl(\exists p>C: p^2 \mid D_i \bigr) \leq \varepsilon,$$where $p$ runs over prime numbers.

**Corollary 12. (Square-freeness conditional on large primes)** _For every $m,n \geq 1$, let $X = X(n,m)$ be a random $n\times n$ matrix with independent entries uniform from $[-m,m]\cap \mathbb{Z}$._ 

_Assume that_ $\{\det(W_{M(n,m)}): n,m \geq 0 \}$ _is known to satisfy a large primes estimate for square-freeness. Then,_ 
$$\lim_{n\to \infty}\lim_{m\to \infty}\mathbb{P}(\det(W_{M}) \textnormal{ is square-free})=\prod_p \Bigl((1+ p^{-1})\prod_{i=0}^\infty (1 - p^{-i-1} ) \Bigr).$$

**Proof.** Note that the events that $p^2 \mid \det(W_M)$ are asymptotically independent over every fixed finite set of primes $p$ as $m\to \infty$. The result hence follows from Lemma 8 by using Theorem 9 to estimate the probability that $\operatorname{coker}(W_M) \otimes (\mathbb{Z}/p^2\mathbb{Z}) \in \{0, \mathbb{Z}/p\mathbb{Z} \}$. $\qed$  

So,  square-freeness of determinants can be reduced to studying the $p$-parts of the cokernel _conditional on a large primes estimate_. (What can be proved concerning large prime estimates is discussed later.) That is, at least for the very special distribution with all entries completely independent and uniform on a large set. 

### Exploiting $\mathbb{Z}[x]$-module structure

What can be said about different random matrix ensembles? The technique that is used to prove Theorem 9 by studying the columns as a stochastic process relies heavily on the uniformity and independence of the entries. It is not so easy to extend this method to different settings. To this end, it turns out to be helpful to use that $\operatorname{coker}(W_M)$ is equipped with richer algebraic structure than just a group.

A matrix $M\in \mathbb{Z}^{n\times n}$ induces a $\mathbb{Z}[x]$-module structure on $\mathbb{Z}^n$ defined by $x v = Mv$ for $v\in \mathbb{Z}^n$. With this definition, the image of the walk matrix is exactly the $\mathbb{Z}[x]$-module span of the all-ones vector: 
$$\operatorname{Im}_{\mathbb{Z}}(W) = \operatorname{span}_{\mathbb{Z}}(M^i e: i\geq 0) = \mathbb{Z}[x]e.$$
Thus, the quotient $\operatorname{coker}(W) = \mathbb{Z}^n/(\mathbb{Z}[x]e)$ is also naturally a $\mathbb{Z}[x]$-module. 

This module structure is useful when extending results to different models. The precise statement is somewhat technical, but it can be simplified subject to a different type of large primes assumption. The ring $\mathbb{Z}[x]$ is two-dimensional and has maximal ideals of the form $\mathfrak{m} = p\mathbb{Z}[x] +  \beta(x)\mathbb{Z}[x]$ with $p$ a prime and $\beta(x)\in \mathbb{Z}[x]$ a polynomial with irreducible reduction in $\mathbb{F}_p[x]$. There are hence "two directions" for the maximal ideals: the prime direction $p$ and the polynomial direction $\beta(x)$.   

The following terminology is not standard, but it is clarifying for our purposes:

**Definition 13.** Fix a prime $p$. For every $d\geq 1$, denote $$\mathcal{B}(p,d):=\{\beta \in \mathbb{F}_p[x] : \beta \textnormal{ is irreducible and }\det(\beta)\geq d \}.$$Then, a collection of random $\mathbb{Z}[x]$-modules $\{{M_i : i\in \cI} \}$ is said to satisfy a _large polynomials estimate at $p$_ if for every $\varepsilon>0$ there exists $d\geq 1$ such that 
$$\max_{i\in \mathcal{I}}\mathbb{P}\Bigl(\exists \beta \in \mathcal{B}(p,d): M_i\otimes\frac{ \mathbb{F}_p[x]}{\beta\mathbb{F}_p[x]} \neq 0 \Bigr)  < \varepsilon.$$

With this notation, we can give a conditional universality result. (Rather, we can give an unconditional result whose statement simplifies conditional on large polynomial estimates.) One more definition is useful to clarify that the entries' law does not matter subject to reasonable constraints, but one can think of nondegenerate $\{0,1 \}$-valued entries as the main example of interest. 

**Definition 14.** A $\mathbb{Z}$-valued random variable $D$ is said to be $\epsilon$-balanced if $$\max_{p}\max_{v\in\mathbb{F_p}}\mathbb{P}(D \equiv v \bmod p)$$   
**Theorem 15. (V.W. [2024](https://arxiv.org/abs/2401.12655))** _Fix some $\epsilon >0$. For every $n\geq 1$, let $M(n)$ be a random $n\times n$ integer matrix whose entries are independent and $\epsilon$-balanced._ 

_Assume that_ $\{\det(W_{M(n)}): n\geq 1 \}$ _satisfies a large primes estimate for square-freeness, and moreover that_ $\{\operatorname{coker}(W_{M(n)}):n\geq 1 \}$ _satisfies a large polynomials estimate at every prime $p$. Then,_
$$\lim_{n\to \infty}\mathbb{P}(\det(W_{M}) \textnormal{ is square-free})=\prod_p \Bigl((1+ p^{-1})\prod_{i=0}^\infty (1 - p^{-i-1} ) \Bigr).$$

We stated that exploiting $\mathbb{Z}[x]$-module structure is essential. To clarify why, we conclude this section with a proof outline. The details of this argument are not needed in what follows in this or the following post. The outline is only given to clarify why the $\mathbb{Z}[x]$-module structure is so important. 

**Proof outline for Theorem 15.** We rely on the _category-theoretic moment method_ of Wood ([2014](https://arxiv.org/abs/1402.5149)) and Sawin-Wood ([2022](https://arxiv.org/abs/2210.06279)).   In classical probability theory, the moment method refers to the fact that the distribution of a $\mathbb{R}$-valued random variable $Y$ can be deduced from its moments $\{\mathbb{E}[Y^n]: n\geq 0 \}$ subject to mild conditions. The category-theoretic moment method implements a similar idea. 

Let $\mathcal{Y}$ be a random algebraic object (say a group or a module). Then, the role of the natural number $n\geq 0$ may be replaced by a fixed finite object $N$. The _$N$-th moment_ of $\mathcal{Y}$ is then the expected number of surjective morphisms to $N$: 
$$m_N := \mathbb{E}[\# \operatorname{Sur}(\mathcal{Y}, N)].$$
The results of Sawin-Wood ([2022](https://arxiv.org/abs/2210.06279)) allow one to recover the distribution of an algebraic object from its moments subject to mild assumptions. (Note: the distribution is only characterized in a _profinite_ topology. This is ultimately why separate large prime and polynomial problems are also necessary.)   

The moment method is a powerful way to study the distribution of cokernels of random matrices. For example, it is relatively tractable to determine the moments of the Abelian group $\operatorname{coker}(M)$ when $M$ is a random matrix with independent entries; see Wood ([2015](https://arxiv.org/abs/1504.04391)). However, the entries of our matrix $W_M$ are not at all independent! The columns of $W_M$ are nontrivial algebraic combinations of the entries of $M$. By instead estimating the moments in the category of $\mathbb{Z}[x]$-modules, we can effectively untwist these algebraic dependencies. 

In particular, by pulling back the morphisms $f:\operatorname{coker}(W_M)\to N$ through the natural quotient map $\mathbb{Z}^n \to \operatorname{coker}(W_M)$, one can show that the $\mathbb{Z}[x]$-theoretic $N$-moment satisfies
$$\mathbb{E}\Bigl[\#\operatorname{Sur}_{\mathbb{Z}[x]}\bigl(\operatorname{coker}(W_M), N \bigr)\Bigr] = \sum_{\substack{F\in \operatorname{Sur}_{\mathbb{Z}}(\mathbb{Z}^n, N)\\ F(e)= 0 } } \mathbb{P}(F\circ M = xF).$$
 Here, the sum runs over surjective group morphisms $F:\mathbb{Z}^n \to N$ with $F(e)=0$.  Note that the problem has been linearized! The probability refers directly to $M$, not to the more complicated matrix $W_M$.  This trick is possible for $\mathbb{Z}[x]$-module moments, but not for moments as Abelian groups.  

One can then analyze the sum on the right-hand side to show that $\mathbb{ E}[\#\operatorname{Sur}_{\mathbb{Z}[x]}(\operatorname{coker}(W_M), N)] \approx (\#N)^{-1}$ and use the category-theoretic moment method to conclude. We refer to [arXiv:2401.12655](https://arxiv.org/abs/2401.12655) for the details. $\qed$

### Undirected graphs

Theorem 15 tells us the probability of square-freeness in digraphs. However, the sufficient condition in Theorem 4 is only applicable to undirected graphs... The sufficient conditions are sensitive to symmetry constraints and numerical evidence suggests that they then apply with different frequency. Some of the key ideas developed surrounding Theorem 15 however also turn out to be applicable in the setting of undirected graphs! 

Recent work of Nikita Lvov and myself ([2026](https://arxiv.org/abs/2603.26932)) studied the satisfaction frequency of arithmetic sufficient conditions for spectral determination in random matrix models with symmetries. The perspective of $\mathbb{Z}[x]$-modules and cokernels will there also be crucial. In particular, while a random matrix model with uniform random integer entries is analytically tractable when all entries are independent (Theorem 9), it is much less tractable if there is a symmetry constraint. It however turns out that an analytically tractable random matrix model could be found by taking uniform random entries from $\mathbb{Z}[x]$. (Or rather, the profinite completion of this ring.)   

Moreover, such $\mathbb{Z}[x]$-theoretic perspectives are also applicable to sufficient conditions different from the walk matrix. Let us discuss one example that will be helpful to connect with the large prime problems in the following section. 

Recall from Theorem 2 and Lemma 6 that, subject to the mild condition that $\det(W)\neq 0$, generalized cospectrality is always realized by conjugacy with a rational orthogonal matrix $Q\in \mathbb{Q}^{n\times n}$ satisfying $Qe = e$. It is natural to wonder what can be said if we only restrict the field of the entries of $Q$ but not the constraint that $Qe = e$. A sufficient conditions for such a notion exists: 

**Theorem 16. (Wang and Yu, [2016](https://arxiv.org/abs/1608.01144))**  _Let $A\in \mathbb{Z}^{n\times n}$ be a symmetric integer matrix with eigenvalues $\lambda_1 \leq \cdots \leq \lambda_n$._ _Then,_ $\Delta_A :=\prod_{i}\prod_{j\neq i} (\lambda_i - \lambda_j)$ _is an integer. Moreover, if_ $\Delta_A$ _is odd and square-free then the only rational orthogonal matrices_ $Q\in \mathbb{Q}^{n\times n}$ _with_ $Q^{T} A Q\in \mathbb{Z}^{n\times n}$ _are in-fact signed permutations._

An alternative proof and generalizations to orthogonal matrices with entries in an arbitrary fixed number field can be found in my recent [2026](https://arxiv.org/abs/2608.12410) work.

As it turns out, the $\mathbb{Z}[x]$-module structure of the cokernel of the matrix $A-xI\in \mathbb{Z}[x]^{n\times n}$ can be used to analyze conditions based on the walk matrix and conditions based on the $\Delta_A$. For example:

**Conjecture 17. (Lvov, V.W., [2026](https://arxiv.org/abs/2603.26932))** _Suppose that_ $A$ _is chosen uniformly at random from all symmetric $n\times n$ matrices with $\{0,1 \}$-valued entries. Then, for every prime $p$,_ 
$$\lim_{n\to \infty} \mathbb{P}(p\nmid \Delta_A) = \Bigl(1-\frac{1}{p}\Bigr) \prod_{k=1}^\infty \Bigl( 1 - \frac{1}{p^{2k}} \Bigr).$$
_Further, for every odd prime $p$,_ 
$$\lim_{n\to \infty} \mathbb{P}\Bigl(p^2 \nmid \Delta_A\Bigr) = \Bigl(1 - \frac{1}{p^2} \frac{3p - 1}{p+1} \Bigr) \prod_{k=1}^\infty \Bigl(1 - \frac{1}{p^{2k}} \Bigr).$$


This conjecture was deduced by proving a variant of it in a different analytically tractable random matrix model. To actually deduce rigorous bounds on the probability of square-freeness, one would consequently also need universality results like Theorem 16 and large prime estimates.

## Large prime estimates

Recall our definition of large prime estimates from Definitions 11 and 13. The fact that such large prime estimates can be a key technical problem in square-freeness estimates is classical in arithmetic statistics, the area of number theory concerned with probabilistic results.

Given an integer polynomial $f\in \mathbb{Z}[x_1,\ldots,x_n]$, large prime estimates on  $f(X_1,\ldots,X_n)$ for an integer polynomial $f$ and $X_i\sim \operatorname{Unif}\{-m,\ldots,m \}$ are a classical challenging topic; see e.g., Hooley ([1967]([https://doi.org/10.1112/S002557930000797X](https://doi.org/10.1112/S002557930000797X))), Nair ([1976](https://doi.org/10.1112/S0025579300008779)), Heath-Brown ([2011](https://arxiv.org/abs/1103.2028)). For a general irreducible polynomial $f$, unconditional results are unfortunately only available in low degree. Extending the range of unconditional results for monic polynomials to degree $d\leq 8$ was one of the results claimed by OpenAI in their preprint dump on October 6 ([2026](https://github.com/openai/math/blob/main/preprints/Squarefree-values-of-quartics-and-power-free-values-of-polynomials-September-24-2026/manuscript.pdf)).     

Granville ([1998](https://doi.org/10.1155/S1073792898000592)) provides estimates for monic polynomials of arbitrary degree conditional on the _abc_-conjecture. Poonen ([2002](https://arxiv.org/abs/math/0203292)) also gives estimates conditional on _abc_ for multivariate polynomials in a slightly modified measure where one of the variables is much larger than the others.  These multivariate results can be applied to $\det(W_M)$ and $\Delta_M$ when $M$ has random integer entries, but only for conditional results.  

Our statistics of interests are however not arbitrary polynomials in the entries of $M$. They have natural interaction with the matrix structure which one may hope to exploit. This has not yet been pursued in the special case of $\det(W_M)$ and $\Delta_M$, but some closely related problems have been investigated. 

The most relevant result are probably those of Nguyen and Wood ([2018](https://arxiv.org/abs/1806.00596), [2022](https://arxiv.org/abs/2210.08526)). They studied the probability that the cokernel $\operatorname{coker}(M)$ of a random matrix is a cyclic group. That is, a group of the form $\mathbb{Z}/n \mathbb{Z}$.  

**Theorem 18. (Nguyen and Wood, [2022](https://arxiv.org/abs/2210.08526))** _Let $M$ be a random symmetric $n\times n$ matrix whose upper-triangular entries_ $\{M_{i,j}:i\geq j \}$ _are i.i.d copies of an integer $\epsilon$-balanced random variable. Then,_ 
$$\lim_{n\to \infty} \mathbb{P}\bigl( \operatorname{coker}(M)\textnormal{ is cyclic}  \bigr) = \prod_{i=1}^\infty \zeta(2i + 1)^{-1} \approx 0.7935\ldots $$
_Here, $\zeta$ is the Riemann zeta function._

Different from most problems considered in previous works on cokernel statistics, this is a "global" problem insofar that it depends on all primes simultaneously. Indeed, a finite Abelian group is is cyclic if and only if $G\otimes \mathbb{Z}/p\mathbb{Z}$ is cyclic for _every_ prime 𝑝. 

The proof by Nguyen and Wood separated the problem in estimates for small primes where cyclicity sometimes fails, and estimates for large primes where cyclicity ultimately does not fail. While the large primes are ultimately insubstantial, proving this is a different story!  The large prime estimates in the proof of Theorem 18 are highly nontrivial and subdivide the largeness in various ranges.  

Note that $\operatorname{coker}(M)$ being cyclic is a necessary condition for $\det(M)$ is square-free. Indeed, recall that the Smith normal form allows us to write $\operatorname{coker}(M) \cong \oplus_i \mathbb{Z}/d_i \mathbb{Z}$ for unique integers $d_1\mid d_2\mid \cdots \mid d_n$ and that $\det(M) = \pm \prod_{i}d_i$. If $d_{n-1} \neq 1$ then $\det(M)$ is not square-free. The cokernel being cyclic is however _not_ a sufficient condition for $\det(M)$ to be square-free. 

For example, it is possible to have $p^2\mid \det(M)$ if the first $n-1$ columns of $M$ span a full rank subspace over $\mathbb{F}_p$ but the final column is divisible by $p^2$. A crucial proof-technical difference between cyclicity and square-freeness is that being cyclic is can be seen from only "mod $p$ considerations" while square-freeness also requires "mod $p^2$ considerations". It is known among experts that ruling out "mod $p^2$ considerations" is extremely difficult. To my knowledge, square-freeness results for $\det(M)$ in the setting of Theorem 18 are hence not currently known. 

One of the only related cases where such issues have been successfully ruled out is in a breakthrough paper by Bhargava, Shankar, and Wang ([2016](https://arxiv.org/abs/1611.09806)) that studied the probability of square-freeness for the discriminant $\Delta_f = \prod_i \prod_{j\neq i}(\lambda_i - \lambda_j)$ of a random monic integer polynomial $f\in\mathbb{Z}[x]$ with independent coefficient. (Here, the $\lambda_i$ are the roots of $f$.) It is possible to have $p^2\mid \Delta_f$ for "mod $p$ considerations"  that only depend on $f\bmod p$ or for "mod $p^2$ considerations" that really require the information in $f\bmod p^2$. The result by Bhargava, Shankhar, and Wang also had a method to rule out "mod $p$^2$ considerations" for large primes. 

# Boosting the probability using fixed-level estimates

Even if one could rigorously prove some version of Conjecture 17 or related conjectures, this in isolation would only give a non-vanishing fraction of graphs is determined by its generalized spectrum.  We known that $\det(W)$ and $\Delta_A$ will _not_ be square-free with probability one. The best that we can hope to establish is a non-vanishing bound on the probability, showing that it is strictly between zero and one.  

However, recall that prime divisors of the level $p\mid \ell$ are square prime divisors of the determinant $p^2\mid \det(W)$ and also that $\ell \mid \det(W)$. This implies that that if the determinant has prime factorization $\det(W) = \prod_{i}p_i^{e_i}$ , then
$$\ell \leq \prod_{i: e_i \geq 2} p^{e_i}.$$
If one could establish that $\det(W)$ was square-free with nontrivial probability, then the same methods would likely be able to show that the prime factorization $\det(W) = \prod_{i}p_i^{e_i}$ has only a few exponents $e_i \geq 2$ and that these are all for small primes. 

Thus, the following conjecture should not be more difficult than the preceding ones: 

**Conjecture 19. (Small levels)** Let $A$ be the adjacency matrix of a random graph on $n$ vertices. Let $\ell\geq 1$ be the greatest level of a rational orthogonal matrix $Q\in \mathbb{Q}^{n\times n}$ with $Q e = e$ such that $Q^T A Q \in \mathbb{Z}^{n\times n}$.  Then, for every $\varepsilon >0$ there exists some $C>0$ such that $\limsup_{n\to \infty}\mathbb{P}(\ell > C) \leq \varepsilon$. 

The following result of Wang and Zhao ([2025](https://arxiv.org/abs/2509.05781)) however rules out small levels: 

**Theorem 20. (Wang and Zhao ([2025](https://arxiv.org/abs/2509.05781)))** Fix some $\ell \geq 2$. Let $G$ be a random graph on $n$ vertices. Then, 
$$\lim_{n\to \infty} \mathbb{P}\bigl(G \textnormal{ has a generalized cospectral mate with level }\ell\bigr) = 0.$$

The proof by Wang and Zhao involves a union bound over all rational orthogonal matrices with a given level.   

Conditional on Conjecture 19, one could use Theorem 20 to prove that almost all graphs are determined by their generalized spectrum.  Thus, one could boost the probability from nonvanishing to one. 

# Conclusion: an outline of a strategy 

The following general strategy for proving bounds on the probability of generalized cospectrality become apparent from the preceding discussion: 
1. Consider some deterministic sufficient condition. 
2. Rephrase the sufficient condition in terms of abstract-algebraic objects associated to a random matrix. 
3. Study the distribution of the local pieces of the algebraic objects that lie over small primes. 
4. Rule out the contribution of the pieces of the algebraic object that lie over large primes.  

This general strategy had been identified in previous works. (See e.g., Sections 1.2 and 1.3 in a [2026](https://arxiv.org/abs/2603.26932) preprint by Nikita and myself.) However, the precise implementation of such a strategy remained a nontrivial open problem. For example, it should be clear that large prime problems remained a highly challenging problem.

 So, what methods were actually used in the preprint [''Almost all graphs are determined by their generalized spectrum''](https://arxiv.org/abs/2610.11047)? This is discussed in the next post. We will see that the high-level scheme of the proof follows the strategy outlined above, but that some new approaches were used to circumvent key bottlenecks. 






[^1]: Algebraic objects associated to random matrices also occur in the study of sandpiles on random graphs, in homology groups for topological data analysis, and in connection to the Cohen-Lenstra heuristics in algebraic number theory. (See Clancy, Kaplan, Leake, Payne, and Wood ([2014](https://arxiv.org/abs/1402.5129)) for the sandpile groups, and see Kahle, Lutz, Newman, and Parson ([2017](https://arxiv.org/abs/1710.05683)) for homology groups, and see Wood  ([2015](https://arxiv.org/abs/1504.04391)) for the Cohen-Lenstra conjectures.) Readers who think that this sounds very exciting may be interested to know that a new online seminar on such topics is being organized by Nikita Lvov and myself at  https://sites.google.com/view/probability-algebra-seminar/


