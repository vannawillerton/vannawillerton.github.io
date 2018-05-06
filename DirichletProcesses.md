---
title: The Dirichlet Process
---

# The Dirichlet Process

## Bayesian Non-parametric Models

In the Generative Models lecture, we talked about 'goodness of fit' of a model to some data. Parametric models using a fixed finite number of parameters may end up with a poor matching between the complexity of the model and the data. Non-parametric approaches fit a single model which adapts it's complexity based on the data given instead of having the complexity of the model given as a parameter, and risk overfitting. Our fundamental goal is to find good models for natural language sentence structure. As we have argued, no finite set of sentences is a good model for natural languages like English. The flexibility of this class of models, where the number of parameters is itself considered a random variable, makes bayesian non-parametrics a good choice for our problem.

One option for defining infinite-dimensional priors over parameters is the Dirichlet Process (DP). This process defines a prior on parameters for a multinomial distribution with an infinite number of (mostly unused) possible outcomes.

## Formal Description of the Dirichlet Process

Recall that a standard probability distribution used over the (K-1)-dimensional simplex is the Dirichlet distribution, defined as follows.

$$p\left(\theta_{1},\ldots ,\theta_{K};\alpha _{1},\ldots ,\alpha _{K}\right)= \frac{1}{B(\vec{\alpha})}\prod _{i=1}^{K}\theta_{i}^{\alpha _{i}-1}$$

## Useful Metaphors

### Polya Urn Process

### Chinese Restaurant Process

### Stick-breaking Process

## Inference Procedure

## Models of Cognition

Bayesian non-parametric models can be useful to linguists and other cognitive scientists, not only as an analysis tool for the complex data dealt with when studying human language, but also as a model of cognition. We can think of the way children adaptively learn to categorize objects from observations in the world as a version of the Chinese Restaurant Process. 

-----------------------------------------------------------
# References 

Anderson, J. (1991). The adaptive nature of human categorization. *Psychological Review*, 98:409-429.

Gershman, S. and Blei, D. (2011). A tutorial on bayesian nonparametric models ...

Hjort, N., Holmes, C., Muller, P., and Walker, S., editors. (2010) *Bayesian Nonparametrics*. Number 28 in Cambridge series in Statistical and Probabilistic Mathematics. Cambridge University Press


-----------------------------------------------------------
# Topics to cover from ProbMods 
1. Introduction and Motivation for non-parametric distributions
..* In section on Generative Models, we talked about 'goodness of fit' of a model to some data. Parametric models using a fixed finite number of parameters may end up with a poor matching between the complexity of the model and the data. We talked about some evaluation metrics for model selection.
..* Non-parametric approaches fit single model which adapts it's complexity based on the data given instead of having the complexity of the model given as a parameter. 
2. Define DPs as a generalization of Dirichlet Distribution
..* Dirichlet Process is a stochastic process, essentially a distribution over distributions.
..* Draws from the Dirichlet Process are themselves discrete distributions over the simplex $$\Theta$$.
..* Parameters $$\alpha$$ (concentration param. Positive real number) and $$H$$ (base distributiob. Distribution over the simplex $$\Theta$$)
3. Describe formally the generative model

4. Constructing a DP with stick-breaking?
5. Constructing a DP with CRP
..* CRP is a prior distribution
..* Sequential sampling scheme using restaurant metaphor
..* Useful properties: simplicity bias (wants fewer customers, tables, assigns N customers to smallest number of tables), rich-get-richer.
6. Pitman-Yor Process (small generalization of CRP with extra param)
7. The Nested Chinese Restaurant Process?
8. Hierarchical DPs?

### Topics to cover from lll
1. How can use of DP processes provide uniform accounts of various aspects of phonological lexicon learning
2.
