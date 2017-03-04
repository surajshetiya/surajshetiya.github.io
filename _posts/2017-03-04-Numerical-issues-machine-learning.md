---
layout: post
title: Numerical issues in Machine learning
---

This is another one of the numerical issues posts which changed the final result while being mathematically correct.


My friend was working on the [Hidden Markov Model](https://en.wikipedia.org/wiki/Hidden_Markov_model) problem where he had found a working code from the github repository.


The glossary for the terms below are as below.

* O - Observation
* $$\pi_{i}$$ - Probability of being in state *i* at time 0
* b_{i}(O_{t}) - Probability of observing the *t*<sup>th</sup> observation from state i


The *alpha*s can be calculated by using the formulae below.

For observation 1 $$\alpha$$, we get the formula below.


$$
\alpha_{1}(i) = \pi_{i}b_{i}(O_{1})
$$


For $$\alpha$$ values at other observations we get the recursive formula below.


$$
\alpha_{t+1}(j) = b_{j}(O_{t+1})\sum_{j=1}^{\N}
$$
