---
layout: single
title: "Graphs as objects associated to spectrum"
date: 2026-11-03 00:00:00 +0000
author: ziqing
---
Author: {{ site.data.authors[page.author].name }}

Most existing literature treats graph spectrum as something obtained from graphs. The goal of this post is to convince you that the converse viewpoint is valid, in other words, graphs can be identified with many different objects associated to spectrum.

**Warning**: Some mild assumptions might be dropped from statements in this post, hence these statements might be slightly incorrect by themselves, and many proofs of the statements in this post are omitted. All graphs are labeled.

## Generalized spectrum

There are many different but equivalent ways to define generalized spectrum, and we adopt the following one in this post.

**Def.** A *generalized spectrum* is a pair $$(\phi, \psi)$$, where $$\phi, \psi \in \mathbb{Z}[x]$$ are of degree $$n$$.

This definition is equivalent to the definition used in the previous post, and a proof is omitted here.

We fix a generalized spectrum $$(\phi, \psi)$$ throughout the post, and always assume that $${\cal G} \neq \emptyset$$ and $$\phi$$ and $$\psi$$ are coprime.

The *graph class* $${\cal G}$$ of a generalized spectrum $$(\phi, \psi)$$ consists of all graphs $$H$$ such that (1) $$\phi$$ is the characteristic polynomial of the adjacency matrix $$A_H$$, (2) $$\psi = e^\top {\rm adj}(x I - A_H) e$$, where $$e$$ is the all $$1$$ vector and $${\rm adj}$$ is the adjugate matrix. The spectral determination problems is asking whether $${\cal G}$$ is of size $$1$$.

## Graphs as isometries

Let us consider the ring $${\cal O} := \mathbb{Q}[x] / (\phi)$$, which is the coordinate ring of the collection of eigenvalues of $${\cal G}$$ viewed as a scheme.

We equipped $${\cal O}$$ the bilinear form on the ring $${\cal O}$$ given by $$\langle x^i, x^j \rangle := w_{i + j}$$, which we call the *walk form*. Here, $$w_i$$ are the numbers such that

$$
\psi / \phi = \sum_{i = 0}^\infty w_i x^{- i - 1}.
$$

It can be shown that $$w_i$$ equals the number of length $$i$$ walks in every $$H \in {\cal G}$$, which explains the name "walk form".

We equipped the ring $$\mathbb{Q}^n$$ the standard bilinear form given by inner product. Then, any graph $$H \in {\cal G}$$ induces a bijective isometry $$\iota_H : {\cal O} \to \mathbb{Q}^n$$ given by $$x^i \mapsto A^i e$$. Moreover, $$\iota_H \circ \ell_x \circ \iota^{-1}_H = \ell_{A_H}$$, as maps $$\mathbb{Q}^n \to \mathbb{Q}^n$$, where $$\ell$$ is the left-multiplication of an element.

Let $${\rm Iso}$$ be the collection of all bijective isometries from $${\cal O} \to \mathbb{Q}^n$$.

**Thm.** There exists a natural embedding from $${\cal G}$$ to $${\rm Iso}$$.

## Graphs as unimodular lattices

Let $${\cal O}_{\mathbb{Z}} := \mathbb{Z}[x] / (\phi)$$ be the integral form of $${\cal O}$$. It is a lattice in $${\cal O}$$, and admits a dual lattice $${\cal O}_{\mathbb{Z}}^\ast$$ in $${\cal O}$$. Here the dual lattice of $$\Lambda \subseteq {\cal O}$$ is

$$
\Lambda^\ast := \{ f \in {\cal O} : \langle f, \Lambda \rangle \subseteq {\cal O}_{\mathbb{Z}}  \}
$$

For every isometry $$\iota : {\cal O} \to \mathbb{Q}^n$$, $$\Lambda := \iota^{-1}(\mathbb{Z}^n)$$ is a lattices sandwiched between the above two lattices:

$$
{\cal O}_{\mathbb{Z}} \subseteq \iota^{-1}(\mathbb{Z}^n) \subseteq {\cal O}_{\mathbb{Z}}^\ast.
$$

Let $${\rm Uni}$$ be the collection of all unimodular (self-dual) lattices $$\Lambda$$ in $${\cal O}$$ such that $$1 \in \Lambda$$ and $$x \Lambda = \Lambda$$.

**Thm.** There exists a natural embedding from $${\rm Iso}$$ to $${\rm Uni}$$.

## Graphs as self-annihilating ideals

Let $${\cal T} := Z[x] / (\phi, \psi) = {\cal O}_{\mathbb{Z}} / (\psi)$$. For a unimodular lattices $$\Lambda \in {\rm Uni}$$, it can be shown that the ideal $$\psi \Lambda / \psi {\cal O}_{\mathbb{Z}} \subseteq {\cal T}$$ is *self-annihilating*, in the sense that its annihilator in $${\cal T}$$ is itself.

Let $${\cal SA}$$ be the collection of self-annihilating ideals of $${\cal T}$$.

**Thm.** There exists a natural embedding from $${\rm Uni}$$ to $${\rm SA}$$.

## Categorical viewpoints

The sets $${\cal G}$$, $${\rm Iso}$$, $${\rm Uni}$$ and $${\rm SA}$$ can all be upgraded to categories (enriched in $$\mathbb{Z}$$ in a cerain way). The natural chain of embedings

$$
{\cal G} \hookrightarrow {\rm Iso} \hookrightarrow {\rm Uni} \hookrightarrow {\rm SA}
$$

is actually a chain of functors. We omit the constructions of the functors on morphisms and their properties.

With this functorial chain of embeddings, in order to show $${\cal G}$$ is of size $$1$$, it is almost possible to work with only $${\rm SA}$$.

In the next post, I will localize $${\rm SA}$$ at each closed point in $${\rm Spec} \mathbb{Z}[x]$$, and show why heuristicaly we should expect that $${\rm SA}$$ is "of size $$1$$ except in a finite region".
