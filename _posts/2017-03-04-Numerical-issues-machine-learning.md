---
layout: post
title: Numerical issues in Machine learning
---

This is another one of the numerical issues posts which changed the final result while being mathematically correct.


My friend was working on the [Hidden Markov Model](https://en.wikipedia.org/wiki/Hidden_Markov_model) problem where he had found a working code from the github repository.


The glossary for the terms below are as below.

* O - Observation
* $$\pi_{i}$$ - Probability of being in state *i* at time 0
* $$b_{i}(O_{t})$$ - Probability of observing the *t*<sup>th</sup> observation from state i
* $$\alpha(i) = P(O_{1}, O_{2}, ... , O_{t}, q_{t} = S_{i}|\lambda)$$ 

In the [forward algorithm](https://en.wikipedia.org/wiki/Forward_algorithm) we need to calculate $$\alpha$$ for each step. The $$\alpha$$s can be calculated by using the formulae below.


For observation 1 $$\alpha$$, we get the formula below.


$$
\alpha_{1}(i) = \pi_{i}b_{i}(O_{1})
$$


For $$\alpha$$ values at other observations we get the recursive formula below.


$$
\alpha_{t+1}(j) = b_{j}(O_{t+1})\sum_{i=1}^{N}\alpha_{t}{i} a_{ij}
$$


Code in python is as below
```python
    def _calcalpha(self,observations):
        '''
        Calculates 'alpha' the forward variable.
    
        The alpha variable is a numpy array indexed by time, then state (TxN).
        alpha[t][i] = the probability of being in state 'i' after observing the 
        first t symbols.
        '''        
        alpha = numpy.zeros((len(observations),self.n),dtype=self.precision)
        
        # init stage - alpha_1(x) = pi(x)b_x(O1)
        for x in xrange(self.n):
            alpha[0][x] = self.pi[x]*self.B_map[x][0]
        
        # induction
        for t in xrange(1,len(observations)):
            for j in xrange(self.n):
                for i in xrange(self.n):
                    alpha[t][j] += alpha[t-1][i]*self.A[i][j]
                alpha[t][j] *= self.B_map[j][t]
                
        return alpha
```


The calculation for $$\alpha$$ has products of previous $$\alpha$$s. Over time we know that this value would become 0 i.e. 0 by the double value. But in order to avoid this situation we need to change the before mentioned logic. Let us look at another approach of doing this.


Let us say we had to compute a product of *A* and *B* which overflows the double or underflows the double. Then how do I represent this in some other format ?


The best way to make sure it is correctly represented is by taking a logarithm of the number.


$$log(A*B) = log(A) + log(B) $$


Hence, by this logic we can take logs on the individual terms and sum them up and yet correctly represent the actual number(we will see that we would normalise later which can be represented in double format).



Let us now look at sum of A and B and see if we can use some similar logic in order to solve the same numerical issues.


$$A + B = X(\frac{A}{X} + \frac{B}{X} $$


By making use of the equation above if we can make sure that the fractions A/X and B/X can be represented in double then we can compute the value of A + B and store it in logarithmic form. LEt us look at the math below.


$$x = log(A)
y = log(B)
$$


We need to compute A + B.

$$A + B = e^{x} + e^{y}$$
