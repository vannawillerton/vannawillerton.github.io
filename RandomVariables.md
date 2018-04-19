---
title: Random Variables
---

# Probability Distributions

We have now seen our first  probability distribution, the distribution over the set $$[ab]^n$$. We have in fact seen two different ways of defining this probability distribution, or *representations* of this distribution, in terms of a sampler and a scorer. In general, there are many different ways of representing a probability distribution. In this part of the course, we will focus on *discrete distributions*, that is, probability distributions whose support consists of discrete elements like integers or symbols. In this setting, the score function is also called a *probability mass function*. We can think of a probability distribution as a set, called the *support*, *sample space*, or *set of outcomes* $$S$$ together with a *probability mass function* $$p$$ which assigns a probability to each element of the support such that all $$p(s) \in [0,1]$$ and $$\sum_{s \in S} p(s) = 1$$. Note that these definitions will not be sufficient if our support is continuous (uncountable), and in that case we will need to make use of measure theory to give a well-defined notion of probability distribution. However, we won't consider these complications in this course. 

# The Bernoulli Distribution

One of the most basic probability distributions is the *Bernoulli distribution* which can be thought of as representing a distribution over a biased coin and is represented by "(flip weight)" where "weight" is the probabilities of heads (or "true"). It is useful to introduce some additional terminology and notation at this point. First, a *random variable* is a mathematical object that takes on a value from some sample space $$S$$ according to some probability mass function $$p$$. For instance, some particular invocation of "flip" constitutes a random variable. 

```
(defn flip [weight]
  (if (< (rand 1) weight)
      true
      false))
(def my-random-variable (flip 0.05))
my-random-variable
```

Importantly, notice two things about the definition of a random variable. First, the random variable is the **particular** call to "flip". While the procedure "flip" defines a distribution, the invocation of this procedure in "(def my-random-variable (flip 0.5))" defines a particular random variable. Second, the random variable refers to the **set** of values that "my-random-variable" can take on, not the particular value of the random variable in any one instance of a program run, which we will call the *value* of the random variable. Random variables can also be more complex objects built from simpler parts. 

```
(def my-random-variable (list (flip 0.5) (flip 0.5)))
my-random-variable
```

Here the random variable of interest is a **list** created by putting together two invocations of "flip". Each particular invocation of "flip" is also a random variable, as well. In general, we will think of any expression built up of samplers and deterministic (non-random) functions as a random variable with the *value* computed by evaluating that expression. Most of the kinds of objects we will be interested in in the course will be complex random variables built up of simpler ones like this.  

Since probability is a tool used across mathematics, engineering, and the sciences, there is a confusing array of different notation and conventions used in different contexts. Here we introduce some of them.

When $$X$$ is a random variable distributed according to some known distribution, such as Bernoulli, we often write the following. 

$$X \sim \mathrm{Bernoulli}(\theta)$$

This is read $$x$$ *is distributed as* a Bernoulli distribution with *parameter* (i.e., weight) $$\theta$$. Another standard notation is to use $$P(X=x)$$ to refer to the probability that random variable $$X$$ takes on value $$x$$. 

$$P(X=\mathrm{\#t}) = \theta$$

Crucially, $$P$$ here should be thought of as a higher-order function which takes a predicate $$X=\mathrm{\#t}$$ and returns the probability that that predicate is true. Often lower case $$p$$ and $$q$$ are used to refer to the probability mass functions associated with random variables, i.e., 

$$P(X=\mathrm{\#t}) = p(\mathrm{\#t}) = \theta$$

Often, people write $$P(X) = \{p(x) | x \in X\}$$ to refer to the whole distribution over the random variable $$X$$. 


# The Categorical Distribution

A *categorical distribution* is the name for a probability distribution over $$k$$ discrete outcomes. It is essentially a $$k$$-sided, biased die. It takes as a parameter a *probability vector* $$\theta$$, of length $$k$$ specifying the probabilities of the $$k$$ possible outcomes. A probability vector is simply a vector whose elements are probabilities $$\in [0,1]$$ which sums to one. 

If $$x$$ is a random variable drawn from a categorical distribution with parameters $$\theta$$, we write. 

$$X \sim \mathrm{categorical}(\theta)$$

## Sampling from a Categorical Distribution
How can we write a sampler for categorical distributions in our language?

```
(defn normalize [params]
  (let [sum (apply + params)]
    (map (fn [x] (/ x sum)) params)))
(normalize (list 2 1 1))

(defn sample-categorical [outcomes params]
  (if (flip (first params))
      (first outcomes)
      (sample-categorical (rest outcomes) 
                          (normalize (rest params)))))

(sample-categorical '(call me Ishmael) (list .5 .25 .25))
```

There are a few new things we have introduced here. First, we have defined a function calles "normalize" which takes a list of numbers and *normalizes* them, i.e. makes it so that they add to $1$. This function uses two new programming ideas.

The first is the "let" statement. The "let" statement gives us a local variable binding and used like this:

"(let [var1 expression1
      var2 expression2
      ...]
  body)"
  
Here "var1" etc. are variables whose values are bound to the values of the correspoding expressions. These variables can then be used in the body of the let statement, whose overall value is the result of evaluating the body. 

The second is the function "apply" which takes a function and a **list** of parameters to that function and applies the function to the list. Why do we use "(apply + params)" in the code above? This is because normally we would call the "+" function with a combination like "(+ 1 2 3)", but here we have access to a **list** called "params" containing the arguments. 

The function "sample-categorical" flips a coin to see if it should return the first object, if the coin comes up true it returns that object. Otherwise, it recurses on the rest of the objects and a **normalized** version of the remaining probabilities. One way to understand this is to realize that the categorical sampler always needs a properly normalized  distribution. But why is the right way to define this? We will see below.
  