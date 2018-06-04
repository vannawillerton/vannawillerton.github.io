---
title: The Dirichlet Process
---

## Bayesian Non-parametric Models

In the Generative Models lecture, we talked about 'goodness of fit' of
a model to some data. Parametric models using a fixed finite number of
parameters may end up with a poor matching between the complexity of
the model and the data. Non-parametric approaches fit a single model
which adapts it's complexity based on the data given instead of having
the complexity of the model given as a parameter. Our fundamental goal is to find good
models for natural language sentence structure. As we have argued, no
finite set of sentences is a good model for natural languages like
English. The flexibility of this class of models, where the number of
parameters is itself considered a random variable, makes bayesian
non-parametrics a good choice for our problem.

One option for defining a prior over infinite-dimensional parameters is
the Dirichlet Process (DP). This process defines a
prior on parameters for a multinomial distribution with an infinite
number of (mostly unused) possible outcomes. The DP is a stochastic
process defining a distributions over distributions. That is, each
draw from a DP is is itself a probability distribution. Just like a
dirichlet distribution, but infinite. The Dirichlet Process is the
best known example of a *non-parametric distribution*. The
term *non-parametric* refers to statistical models whose size or
complexity can grow with the data, rather than being specified in
advance.

Just as the Dirichlet Distribution is a distribution over a k-sided die,
you can imagine the DP as a distribution over an infinite-sided die.
Now you may wonder how one would define an infinite-sided die. We will see
how to do this using the stick-breaking process, below.

## Constructing the Dirichlet Process

#### Stick-Breaking Process

The stick-breaking process is an intuitive way to visualize draws from
a DP. Imagine drawing an infinite sequence of samples from a Beta
distribution with parameters 1, $$\alpha$$ (recall that the Beta
distribution is a Dirichlet distribution over the 1 dimensional
simplex). We write this infinite set of draws as
$${\beta_k'}_{k=1}^{\infty}$$.

$$\beta_k' \sim Beta(1,\alpha)$$

Ultimately we would like to define a distribution on an infinite set
of discrete outcomes that will represent categories or mixture
components, but we start by defining a distribution on the natural
numbers. The probability of the natural number $$k$$ is given by:

$$\beta_k = \prod^{k-1}_{i=1} (1-\beta_i')\cdot\beta_k'$$

Now imagine "walking" down the natural numbers in order, flipping a coing with
weight $$\beta_i'$$ for each natural number $$i$$. If at some $$i$$, the coin 
comes up false, we continue to the next natural number; if the coin comes up true,
we stop and return the natural number index we halted on. 

Going back to our die analogy, if we flipped true when we reached some number $$k$$, 
we would say that we rolled the die and the side $$k$$ came out on top.

This is only one of many ways of constructing the DP. Another very useful one 
is the Chinese Restaurant Process, which we will see below.

## Formal Description of the Dirichlet Process

#### Dirichlet Distribution

Recall that a standard probability distribution used over the
(K-1)-dimensional simplex is the Dirichlet distribution, defined as
follows.

$$p\left(\theta_{1},\ldots ,\theta_{K};\alpha _{1},\ldots ,\alpha _{K}\right)= \frac{1}{B(\vec{\alpha})}\prod _{i=1}^{K}\theta_{i}^{\alpha _{i}-1}$$

In order to understand the definition of the DP as an
infinite-dimentional prior, it is important to note that the Dirichlet
distribution satisfies conditions for the expansion rule, which can be
used to increase the dimentionality of a Dirichlet distribution. Let $$(p_1,\ldots,p_K \sim \mathrm{Dirichlet}(\alpha_1,\ldots,\alpha_K)$$ and $$\theta \sim \mathrm{Beta}(\alpha_1b,\alpha_1(1-b))$$ for $$0 < b < 1$$. Then one dimension of the Dirichlet distribution can be split into two dimensions as follows:

$$(p_1\theta,p(1-\theta),p_2,\ldots,p_K) \sim \mathrm{Dirichlet}(\alpha_1b,\alpha_1(1-b),\alpha_2,\ldots,\alpha_K$$

Repeatedly splitting a Dirichlet distributions into components based
on the expansion rule gives the following, where K is the number of
components.

$$p^{(K)} \sim \mathrm{Dirichlet}(\frac{\alpha}{K},\ldots,\frac{\alpha}{K})$$

Taking the limit as K goes to infinity gives a prior over an infinite-dimensional space.

#### Dirichlet Process

We may now define the DP. As previously stated, we take the limit as K goes to infinity.

$$p \sim \lim_{K\to\infty}\mathrm{Dirichlet}(\frac{\alpha}{K},\ldots,\frac{\alpha}{K})$$

For each point in this distribution, we assign a value drawn from a
base distribution $$H$$. If G is a random distribution drawn from this
Dirichlet process, then:

$$G = \sum_{k=1}^{\infty} p_k\delta_{\theta_k}$$
**So, I think it is worth making it clear that the base distribution
is just the distribution on labels on our infinite-sided die. FWIW I
never find the notation above particularly clear. Since it uses $\sum$
in a way that could bear some explaining (it is essentially an $\vee$
or something --- it represents the set of choices in the
distribution.**

Where $$p_k$$ is the probability assigned to the kth point, $$\delta$$
is the point mass of some location and $$\theta_k$$ is the value or
location of some point. In other words, if G is a random distribution
drawn from the process defined above, then it is an infinite discrete
distribution over the same space as base distribution H.**note that
this is something which is not obvious, when they say this, it is
because it was a result in the original ferguson paper** Thus we have
defined the dirichlet process and write:

$$G \sim DP(\alpha, H)$$

As you can see, the DP is parameterized by $$\alpha$$ and $$H$$. $$H$$
is the base distribution. Since the DP is a measure on distributions, H is the mean distribution. $$\alpha$$ is a concentration parameter (for higher values of $$\alpha$$, the probability mass will
concentrate more tightly around the mean).

In this way it is easy to
show the existence of the DP by considering some finite measurable
partition of $$\Theta$$, $${A_1,\ldots,A_K}$$. If $$G \sim DP(\alpha,
H)$$, then every measurable partition of $$\Theta$$ is Dirichlet
distributed.

$$(G(A_1),\ldots,G(A_K)) \sim Dir(\alpha H(A_1),\ldots,\alpha H(A_K))$$

It is important to note that in practice all but a finite subset will **not** be used. The amound of components used in the end should reflect a the complexity of the data.

## Useful Constructions

Understanding the DP can be difficult, but a number of constructions may help to highlight some key properties.

### Chinese Restaurant Process
The Chinese Restaurant Process (CRP) is a more complex and widely used
construction for understanding the Dirichlet Process. It is important to
note that these are alternative but equivalent ways to
construct the Dirichlet process. The CRP is usually described as a
sequential sampling scheme using the metaphor of a restaurant.

We imagine a restaurant with an infinite number of tables. The first
customer enters the restaurant and sits at the first unoccupied table.
The (N + 1)th customer enters the restaurant and sits at either an
already occupied table or a new, unoccupied table, according to the
following distribution.

$$\tau^{(N+1)}|\tau^{(1)},\ldots,\tau^{(N)},\alpha \sim 
\sum_{i=1}^K \frac{y_i}{N+\alpha}\delta_{\tau_i}+
\frac{\alpha}{N+\alpha}\delta_{\tau_{K+1}}$$

$$N$$ is the total number of customers in the restaurant. $$K$$ is the
total number of occupied tables, indexed by $$K\leq i\leq 1$$.
$$\tau^{(j)}$$ refers to the table chosen by the $$j$$th customer.
$$\tau_i$$ refers to the $$i$$th occupied table in the restaurant.
$$y_i$$ is the number of customers seated at table $$\tau_i$$.
Finally, $$\delta_\tau$$ is the $$\delta$$-distribution which puts all
of its mass on table $$\tau$$.

More intuitively, customers sit at a table which is already occupied
with probability proportional to the number of individuals already
seated at that table. Customers sit at a new table with probability
controlled by the concentration parameter $$\alpha$$.

Each table has a *dish* associated with it. Each dish $$v$$ acts as a
label on the table; it is shared by all customers seated at that
table. When the first customer sits at a new table, $$\tau_i$$, a dish
is sampled from the base distribution $$H$$ and is placed on that table.
From then on, all customers who are seated at table $$\tau_i$$ share
the sampled dish $$v_{\tau_i}$$.

One way of understanding the CRP is to think of it as defining a
distribution over ways of partitioning $$N$$ items (customers) in to
$$K$$ partitions (tables), for all possible $$N$$ and $$K$$.

The probability of a particular partition of $$N$$ customers over
$$K$$ tables is the product of probabilities of the $$N$$ choices made
in seating those customers. It can easily be confirmed that the order
in which elements are added to the partition components does not
affect the probability of the final partition. That is, the terms of
the product can be rearranged in any order. Thus the distribution
dfined by a CRP is exchangeable.

**So the CRP is related to the DP just like the polya urn scheme is
related to the Dirichlet distribution. I.e., the CRP is the posterior predictive distribution
when you integrate out draws from the DP. You can look through the
notes on the Polya urn scheme from the lectures**
 
#### Key Properties of the DP

The CRP construction helps to highlight some properties of the DP. The
first is that the CRP implements a simplicity bias. It assigns a
higher probability to partitions which (1) have fewer customers, (2)
have fewer tables, and (3) for a fixed number of customers N, favors
assigning them to the smallest number of tables.

Thus the CRP favors simple restaurants and implements
a *rich-get-richer* scheme, or self-reinforcing property. Because
customers sit at a table with a probability proportional to the number
of customers already at the table, it should be clear that tables with
more customers have higher probability of being chosen by later
customers. These properties mean that, all else being equal, when we
use the CRP, we will favor reuse of previously computed values.

### Blackwell-MacQueen Urn Scheme

A final visualization of Dirichlet process and chinese restaurant
process comes from an extension of the Polya urn scheme which allows a
continuum of colors.

Imagine that you start with an urn filled with $$\alpha$$ black balls.
You then follow the following sampling scheme. At each step, draw a
ball from the urn, then:

1. If the ball is black, sample a new color from base distribution
$$H$$, label a *new* ball with this colour, and put both balls back in
the urn.

2. If the ball is some non-black colour, label a new ball with the
same colour, and put both balls back in the urn.

This construction is the same as the Polya urn scheme except for the fact that the Polya urn scheme allows for draws from some finite set of colours X, while the Blackwell-MacQueen Urn scheme is not restricted to finite X. (Number of colours in the urn could be infinite).

Convince yourself that the resulting distribution over colours will be
the same as the distribution over tables in the Chinese restaurant
process.

-----------------------------------------------------------
# References 

Anderson, J. (1991). The adaptive nature of human
categorization. *Psychological Review*, 98:409-429.**I think that
Anderson accidentally defined something which looked like the CRP
here**

Gershman, S. and Blei, D. (2011). A tutorial on Bayesian nonparametric models ...

Hjort, N., Holmes, C., Muller, P., and Walker, S., editors.
(2010) *Bayesian Nonparametrics*. Number 28 in Cambridge series in
Statistical and Probabilistic Mathematics. Cambridge University Press.

Xing, E. “Bayesian Nonparametrics: Dirichlet Processes” Probabilistic
Graphical Models, 10-708, Spring 2014, lecture.

http://v1.probmods.org/non-parametric-models.html

https://en.wikipedia.org/wiki/Dirichlet_process
