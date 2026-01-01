---
layout: post
title: "Random Graphs, pt. 1"
tags: [Math, Random graph theory]
published: true 
---

It is probably clear to most math/CS interested people why studying 'networks' or graphs are important for real-world applications. Aside from differential equations, graph theory is probably one of the most well applied subjects in an undergraduate math curriculum, stemming largely from the massive communication networks of the Information Age, as well as the recent surge in popularity of AI and machine learning. (Please don't fact check that.)

When we want to analyze such massive graphs, however, with potentially millions of vertices and billions of edges, we need to meaningfully summarize the information contained in these graphs. The approach taken by 'network theorists' is to study *probabilistic descriptions* of *local quantities* on these graphs. This motivates <u>random graph theory</u>, which is a subtopic at the intersection of combinatorics and probability theory that broadly studies properties of randomly generated graphs or stochastic processes on graphs, random or otherwise.

I want to record some of my notes from [van der Hofstad's *Random Graphs and Complex Networks*](https://rhofstad.win.tue.nl/NotesRGCN.html) (*RGCN*), a wonderful book I've started reading (very slowly) earlier this year. 

<div style="text-align: center; margin: 5%;">
	<a href="https://www.cambridge.org/core/books/random-graphs-and-complex-networks/AA6578462E56868A874B083E082C9FE7?utm_campaign=shareaholic&utm_medium=copy_link&utm_source=bookmark">
		<img src="/assets/images/RGCN_vol1_cover.jpg" alt="Cover of van der Hofstad's Random Graphs and Complex Networks, volume 1" loading="lazy">
	</a>
</div>


Here is material from the start of Chpt. 1 of *RGCN*. This chapter mostly motivates and defines topics covered later in the text.

## 1.1 Degree and connectivity

Recall that a graph $$G = (V, E)$$ is a collection of vertices $$V$$ and edges between them, $$E$$. 

Since we want to study "local quantities" of these graphs, which is to say, what properties look like in the neighborhoods around their vertices, and we would like to describe these probabilistically, we need to talk about sampling vertices.

(We will assume, as some topics in random graph theory do, that our graphs have $$n$$ vertices and we send $$n \to \infty$$ so we can safely think of graphs with finitely many vertices although we are modelling arbitrarily large real-world networks.)

Consider the following two natural ways of sampling vertices from an undirected, simple graph $$G = (V, E)$$

  1. Uniformly over $V$
	
  2. Uniformly select an edge in $E$, then uniformly choose an incident vertex of that edge

Here, we'll record a few basic general statements about degrees of vertices selected randomly as above from deterministic graphs.

Write $$D = \deg(U)$$ where $$U \sim \text{Uniform}(V)$$ as in entry 1 above. This is also called *typical degree* of a graph.

Write $$D^*$$ for the degree of a vertex selected by the procedure described in entry 2, which *RGCN* refers to as "random friendship" selection.

**Lemma:** Let $$G = (V, E)$$ with $$\lvert V\rvert = n$$. Then we have

\\[
	P(D^* = k) = \displaystyle \frac{k \cdot P(D = k)}{\mathbb{E}[ D]}
\\]

*Proof:* Consider the *directed* graph formed by splitting the edges of $$G$$, $$G_{\text{split}} = (V, E_{\text{split}})$$ where $$\\{u, v\\} \in E \iff (u, v)$$ and $$(v, u) \in E_{\text{split}}$$.

We can check that the random variable given by uniformly selecting an edge $$e = (u, v)$$ of $$G_{\text{split}}$$ and taking the outdegree of the destination vertex of $$e$$, $$v$$, has the same distribution as $$D^*$$. For convenience, we write $$D^*$$ to mean this other random variable with the same distribution.

Then, each $$v \in V$$ contributes $$\deg( v)$$ edges to $$E_{\text{split}}$$ that point into $$v$$, which means that if they are selected, $$D^*$$ attains the value $$\deg (v)$$. Therefore we have
\\[
	P(D^* = k) = \displaystyle \frac{k \cdot \lvert \\{v \in V : \deg(v) = k\\} \rvert}{\sum\limits_{i \in \mathbb{N}} i \cdot \lvert \\{v \in V : \deg(v) = k\\} \rvert} = \displaystyle \frac{k \cdot P(D = k)}{\mathbb{E}[D]}
\\]

which is exactly the desired identity. $$\square$$

In light of this last lemma, I think of $$D^*$$ as counting vertices more based on their contributions to $$D$$. This is because the identity gives the only possible mass for a random variable with $$P(D^* = k) \propto k \cdot P(D = k)$$. In general, what we did to $$D$$ in order to get $$D^*$$ is known as 'size-biasing' a random variable.


Definition: Let $$X$$ be a nonnegative random variable with $$\mathbb{E}[X] > 0$$. We define the <u>size-biased</u> version of $$X$$, $$\underline{X^*}$$, to be the random variable with distribution
\\[
P(X^* \leq x) = \displaystyle \frac{ \mathbb{E}[X \cdot \mathbb{1}_{X \leq x}]}{\mathbb{E}[x]}
\\]


We can show this definition agrees with the previous lemma in fact for any nonnegative, discrete r.v. $$X$$ by linearity of expectation, writing $$\mathbb{1}_{X \leq x} = \mathbb{1}_{X \leq x - 1} + \mathbb{1}_{X = x}$$, and using additivity of $$P$$.


**Proposition:** $$\mathbb{E}[D^*] \geq \mathbb{E}[D]$$ if $$D$$ has positive expectation.

*Proof:* By the lemma above and the definition of expected value,

$$
\begin{align*}
	\mathbb{E}[D^*] &= \sum\limits_{k=0}^\infty k \cdot P(D^* = k) \\\\
					&= \sum\limits_{k=0}^\infty \displaystyle \frac{k^2 \cdot P(D = k)}{\mathbb{E}[D]} = \displaystyle \frac{\mathbb{E}[D^2]}{\mathbb{E}[D]}
\end{align*}
$$

By the definition of variance, we have $$\mathbb{E}[D^2] = \mathbb{E}[D]^2 + \text{Var}(D)$$ so that

\\[
	\mathbb{E}[D^*] = \mathbb{E}[D] + \displaystyle\frac{\text{Var}(D)}{\mathbb{E}[D]} \geq \mathbb{E}[D]
\\]

where the last inequality follows from variance being nonnegative. Furthermore, since $$\text{Var}(D) = 0$$ if and only if $$D$$ is deterministic, which is equivalent to saying $$G$$ is $$k$$-regular, we have $$\mathbb{E}[D^*] \geq \mathbb{E}[D]$$ with equality iff $$G$$ is $$k$$-regular for some $$k$$. $$\square$$

There is still more from this section, but this post has gotten long, so I'll end this one here. Stay tuned for the next post on random graphs where we prove that you have no friends (relative to your friends).
