---
title: Random Variables
---

# Probability Distributions

We have now seen our first  probability distribution, the distribution over the set $$[ab]^n$$. We have in fact seen two different ways of defining this probability distribution, or *representations* of this distribution, in terms of a sampler and a scorer. In general, there are many different ways of representing a probability distribution. In this part of the course, we will focus on *discrete distributions*, that is, probability distributions whose support consists of discrete elements like integers or symbols. In this setting, the score function is also called a *probability mass function*. We can think of a probability distribution as a set, called the *support*, *sample space*, or *set of outcomes* $$S$$ together with a *probability mass function* $$p$$ which assigns a probability to each element of the support such that all $$p(s) \in [0,1]$$ and $$\sum_{s \in S} p(s) = 1$$. Note that these definitions will not be sufficient if our support is continuous (uncountable), and in that case we will need to make use of measure theory to give a well-defined notion of probability distribution. However, we won't consider these complications in this course. 

# The Bernoulli Distribution

One of the most basic probability distributions is the *Bernoulli distribution* which can be thought of as representing a distribution over a biased coin and is represented by "(flip weight)" where "weight" is the probabilities of heads (or "#t"). It is useful to introduce some additional terminology and notation at this point. First, a *random variable* is a mathematical object that takes on a value from some sample space $$S$$ according to some probability mass function $$p$$. For instance, some particular invocation of "flip" constitutes a random variable. 

