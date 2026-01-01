---
layout: post
title: "L^p Spaces and their Duals"
tags: [Math, Analysis]
published: false
---

The Fall semester just ended and I've wanted to start writing a blog for a while--since my friends encouraged me to do so in the Summer--so here's the first post. I will hopefully post typed-up notes and other projects on here. I wasn't really sure what to post about here, so I'll write about a few things from *Real Analysis, MA540*, a class I took last semester.

Recall that a *Banach space* $$(X, \|\cdot\|)$$ is a normed vector space that is complete with respect to the metric space induced by its norm: $$(X, d)$$ where $$d$$ is given by $$d(x, y) = \|x - y\|$$.

An obvious example is $$\mathbb{R}^n$$ over $$\mathbb{R}$$ with, for example, the Euclidean norm 
\\[
{||x||}\_2 = (\sum\limits_{i=1}^n x_i^2)^{\frac{1}{2}}
\\]
which is also called the $$\ell_2$$ norm. We get the $$\ell_p$$ norm if we replace the $$2$$ and $$\frac{1}{2}$$ in the definition of the Euclidean norm with $$p$$ and $$\frac{1}{p}$$.

Since we introduced a metric and some topological conditions on our space $$X$$, you would be right to guess that I want to talk about some analytic considerations. (Also, I did say I would write about *real analysis*.) But, as my linear algebra professor said, when we define vector spaces we're really more interested in morphisms between them, which is to say linear maps. Therefore, I need to introduce the main characters of our story, the maps we're going to be interested in.

Now, recall from linear algebra the definition of the *algebraic dual space* of $$V$$, which is the collection of linear functionals on $$V$$:
\\[	
V^* := \\{f: V \to \mathbb{R} \mid f \text{ is linear}\\}
\\]
If we go back to our example of $$\mathbb{R}^n$$ (or, of course, any finite-dimensional real or complex vector space), using more basic linear algebraic theorems it is not hard to prove that $$V \cong V^*$$ by a dimension argument. If we fix a basis $$\beta$$ of $$V$$, we can form a dual basis $$\beta^*$$ by taking basis vectors $$b_i \mapsto b_i^* := \delta_{ij} \text{ on } b_j$$ and extending to the unique linear extension on $$V$$ (since $$V$$ is finite dimensional).

I like to think of linear functionals as shadows that a vector $$v$$ casts on its environment from a given direction $$b_i$$. If we only know what $$b_i^* v$$ looks like for one $$i$$, we don't have enough to guess what $$v$$ is. But if you know what the shadow of $$v$$ looks like from <u>sufficiently many, different</u> directions, we are able to sketch $$v$$ well enough to exactly determine what it is. 

However, this last heuristic kind of falls apart when we get to infinitely many dimensions. First of all, my definition of the dual $$v^*$$ of a vector $$v$$ relied on $$\dim V < \infty$$ to uniquely complete it to all of $$V$$. If you noticed "Hey! $$b_i^*$$ looks like $$\left< \cdot, b_i \right>$$, can we use that instead?" while you would be correct to say this, it turns out that forcing an inner product to compatible with our notion of Banach spaces is a little **too** stron for our purposes. (This gives you what is called a (Hilbert space)[https://e.math.cornell.edu/people/belk/measuretheory/HilbertSpaces.pdf], which is also a useful definition.)

In infinite dimensions, this '$$n$$ shadows determines a vector' idea is doomed to fail. 
