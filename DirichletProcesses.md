---
title: The Dirichlet Process
---

# The Dirichlet Process

## Bayesian Non-parametric Models

In the Generative Models lecture, we talked about 'goodness of fit' of a model to some data. Parametric models using a fixed finite number of parameters may end up with a poor matching between the complexity of the model and the data. Non-parametric approaches fit a single model which adapts it's complexity based on the data given instead of having the complexity of the model given as a parameter, and risk overfitting. Our fundamental goal is to find good models for natural language sentence structure. As we have argued, no finite set of sentences is a good model for natural languages like English. The flexibility of this class of models, where the number of parameters is itself considered a random variable, makes bayesian non-parametrics a good choice for our problem.

One option for defining infinite-dimensional priors over parameters is the Dirichlet Process (DP). This process defines a prior on parameters for a multinomial distribution with an infinite number of (mostly unused) possible outcomes.

## Formal Description of the Dirichlet Process

#### Dirichlet Distribution

Recall that a standard probability distribution used over the (K-1)-dimensional simplex is the Dirichlet distribution, defined as follows.

$$p\left(\theta_{1},\ldots ,\theta_{K};\alpha _{1},\ldots ,\alpha _{K}\right)= \frac{1}{B(\vec{\alpha})}\prod _{i=1}^{K}\theta_{i}^{\alpha _{i}-1}$$

In order to understand the definition of the DP as an infinite-dimentional prior, it is important to note that the Dirichlet distribution satisfies conditions for the chain rule, which can be used to increase the dimentionality of a Dirichlet distribution. 

Repeatedly splitting a Dirichlet distributions into components based on the chain rule gives:

$$p^{(K)} &\sim& \mathrm{Dirichlet}(frac{\alpha}{K},\ldots,frac{\alpha}{K})$$

Taking the limit as K goes to infinity gives a prior over an infinite-dimensional space.

#### Dirichlet Process

We may now define the DP.

$$p &\sim& \lim_{K\to\infty}\mathrm{Dirichlet}(frac{\alpha}{K},\ldots,frac{\alpha}{K})$$

For each point in this Dirichlet distribution, we assign a value drawn from a base distribution $$H$$. If G is a random distribution drawn from this Dirichlet process, then:

$$G = \sum_{k=1}^{\infty} p_k\delta_{\theta_k}$$

Where $$p_k$$ is the probability assigned to the kth point and $$\theta_k$$ is the value of that point. Thus we have defined the dirichlet process and write:

$$G &\sim& DP(\alpha, H)$$

The DP is parameterized by $$\alpha$$ and $$H$$. $$\alpha$$ is a concentration parameter (for higher values of $$\alpha$$, the probability mass will concentrate more tightly around the mean), and $$H$$ is the base distribution (essentially the mean).

The way we have defined it builds up from finite dimentional distributions. In this way it is easy to show the existence of the DP by considering some finite measurable partition of $$\Theta$$, $${A_1,\ldots,A_K}$$. If $$G &\sim& DP(\alpha, H)$$, then every measurable partition of $$\Theta$$ is Dirichlet distributed,

$$(G(A_1),\ldots,G(A_K)) &\sim& Dir(\alpha H(A_1),\ldots,\alpha H(A_K)).

It is important to note that in practice not all of the infinite components of the dirichlet process will need to be used. Only the components which are reflected in the data will be used, but unlike in parametric models there is flexibility, which can help to avoid overfitting and underfitting problems.

## Useful Metaphors

understanding the DP can be difficult, but a number of useful metaphors may help to highlight some key properties.

### Polya Urn Process

### Chinese Restaurant Process

### Stick-breaking Process

## Inference Procedure


-----------------------------------------------------------
# References 

Anderson, J. (1991). The adaptive nature of human categorization. *Psychological Review*, 98:409-429.

Gershman, S. and Blei, D. (2011). A tutorial on bayesian nonparametric models ...

Hjort, N., Holmes, C., Muller, P., and Walker, S., editors. (2010) *Bayesian Nonparametrics*. Number 28 in Cambridge series in Statistical and Probabilistic Mathematics. Cambridge University Press.

Xing, E. “Bayesian Nonparametrics: Dirichlet Processes” Probabilistic Graphical Models, 10-708, Spring 2014, lecture.
