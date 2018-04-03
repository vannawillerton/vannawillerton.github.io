---
title: Models of Computation
---


How does language work? This is the foundational question which motivates the field of linguistics. The modern study of language or *generative linguistics* began in the late 1940s and early 1950s when it was realized that the emerging understanding of computation that resulted from the work of Kurt Gödel, Alan Turing, Alonzo Church, Emil Post, Rózsa Péter, Stephen Kleene and others might be able to shed light on this question. 

These researchers had begun to explore simple *machine models* of computation such as the Turing machine, Post rewrite systems, the $$\mu$$-recursive functions, and the $$\lambda$$-calculus. These models were originally intended to formalize the notion of *mathematical computation* or the reasoning processes used by a mathematician in proving theorems in a step-by-step fashion. Two surprising facts were soon discovered. First, Turing machines, $$\lambda$$-calculus, and other systems so-introduced proved to be equivalent in the sense that they could be used to define exactly the same set of functions. It was conjectured that this set of formalisms, the *Turing-complete* formalisms,  in fact defined the maximal set of function that could be *effectively computed*&mdash;that is, actually implemented in real physical hardware (this conjecture is known as the *Church-Turing thesis*).  Second, it was discovered that there existed particular machines in each formalism which were *universal computers*. These machines could be programmed using their input to simulate the behavior of any other machine in the class. In modern terms, these machines are interpreters able to perform any computation definable by a Turing machine.

These discoveries, which occurred in the 1930s launched the modern theory of computation. It wasn't long before researchers began to realize that such models might have applications in modeling more general processes of the human mind beyond theorem proving. In particular, beginning in the early 1950s researchers such as Yoshua Bar Hillel, Charles Hockett and, most notably, Noam Chomsky, began to apply and adapt these tools to understanding how language might be produced and comprehended. 

In another thread of research, Claude Shannon began studying the problem of transmission of information under conditions of uncertainty, and laid the foundations for the modern field of *information theory*. These tools were also quickly adapted to be used in the study of problems of the mind by researchers such as George Miller, and in the case of language, Charles Hockett. 

The ideas of  these early researchers still form the foundations the modern fields of linguistics, artificial intelligence, and natural language processing. In this course, we will study these foundations with the goal of understanding the logic of how the tools can be applied to build models of language. Along the way, we will acquire many of the conceptual tools still needed to read the modern literature in natural language processing. However, the goal is not only to understand how such models work, but to be able to critically evaluate how computational models advance our scientific understanding of language. 

But first, we need a model of computation....

# The $$\lambda$$-Calculus and LISP

In this course, we will use the lambda calculus as our basic model of computation. The $$\lambda$$-calculus was introduced by Alonzo Church in the 1930s as a computable model of mathematical logic. Church based this model on mathematical *functions* applied to arguments, building up complex computable functions (originally representing logical expressions) from simple ones. In his famous paper introducing the Turing machine, Alan Turing showed that Church's $$\lambda$$-Calculus and Turing machines were equivalent in the sense that they computed the same set of functions. In  1960, John McCarthy introduced LISP, one of the first practical programming languages, based on the $$\lambda$$-Calculus using list-based data structures (hence the name LISt Processor).

LISP was the first programming language in the paradigm that became known as *functional programming* which now includes languages such as Haskell, ML, Erlang, and many aspects of imperative programming languages (e.g., Guy Steele, the designer of Java, also was the designer of the LISP dialect we will use in this course). The behavior of functional programs is often easier to reason about than imperative programs and easier to parallelize. Thus, these languages have become important again in recent years after a period of less popularity. Functional languages also form the basis for most *probabilistic programming languages*&mdash;high-level programming languages that make it easy to specify probabilistic models. The [Church](http://projects.csail.mit.edu/church/wiki/Church) programming language is one inspiration for this course.  The $$\lambda$$-calculus is also the main computational tool used in formal semantics as studied in linguistics. Thus, a thorough understanding of the $$\lambda$$-calculus will be helpful in many areas beyond this course. 

We will use a variant of LISP called [Clojure](https://clojure.org/). Althought the language is very powerful, the basic syntax of Clojure is very simple and can be learned in a few minutes. In the next few sections, we will discuss the basics of Clojure, before proceeding to use the language to begin our study of language using these tools. 

## Function Application

The most important operation in the  $$\lambda$$-calculus is the application of a function (also called a *procedure* in LISP) to some arguments. In LISP procedure application is expressed in Polish notation like so: (function argument1 argument2). For example, we can add 1 and 2 as follows. 

```
(+ 1 2)
```

There are a few things to note about the example above. First, this kind of expression which starts with an open parenthesis, the name of a procedure, some number of arguments, and a close parenthesis is called a *combination* and is the way we instruct the interpreter to apply a function.  

Computing the output of this expression is called *evaluation* in LISP, and is performed by a primitive procedure called "eval". In this case, the result is the *value* "3". In general, in functional programming languages every well-formed expression has a value. Because 
 "+" is a *primitive procedure*&mdash;that is, a procedure built into the language&mdash;and "1" and "2" are *constants* with the *primitive type* of *integer*, it is easy to evaluate this expression. Of course the true power of LISP, like any programming language, comes from the ability to define new procedures that perform new computations, not just use existing primitives. The operator that allows the definition of new functions in the $$\lambda$$-calculus is called $$\lambda$$ and is what gives the  $$\lambda$$-calculus its name. In Clojure we write "fn" instead of $$\lambda$$. The general form of a $$\lambda$$ expression in Clojure looks like this:  "(fn [...parameters...] ...body...)". 

```
(fn [x y] (+ x y))
```

Note what happens when we evaluate the expression above. The value of a "lambda"/"fn" expression is a function. 

Let's take a look at the definition above. It has three parts. First, there is the  "fn" operator. Second, there is a list of *formal parameters* to the procedure. These are variables that will hold the values of inputs to the procedure. In this case, this includes "x" and "y". Third there is the procedure *body* which expresses the computation performed by the procedure. In this case, the body simple adds the values stored in the two variables. 

How can we use a $$\lambda$$-defined procedure? Consider the following example. 

```
((fn [x y] (+ x y)) 1 2)
```

This is a little hard to parse at first, but with a little effort you can see that this code snippet is similar to "(+ 1 2)" but with "+" replaced with the procedure definition "(fn [x y] (+ x y))". In this example, the procedure is constructed and them immediately applied to the arguments "1" and "2" to compute the output value "3", and then "forgotten" by the interpreter. How can we make a function that doesn't disappear?

## Naming things with "def"

In Clojure we can create named variables with the "def" primitive. 

```
(def x 1)
```

"def" *binds* the value "1" to the variable called "x".

```
(def x 1)
(+ x x)
```

Now when we run the expression "(+ x x)" the interpreter first looks up the value of the variable "x" and then applies the function "+" to this value (twice). We can also use "def" to name functions created with "fn".

```
(def my-addition (fn [x y] (+ x y)))
```
Now we have a function named "my-addition" which is defined using the "fn" term we introduced above. Note an important fact, for Clojure there is no difference between binding a number like "1" to a variable-name like "x" or a function to a variable name like "my-addition". Functions are *first class*, they are simply a type of object in the system like any other.  

```
(def my-addition (fn [x y] (+ x y)))
(my-addition 1 2)

(def x 1)
(my-addition x x)
```

Because we very frequently need to define procedures, Clojure provides a shorthand for doing this. Instead of writing "(def my-addition (fn [parameters] body))" in Clojure we can also write "(defn my-addition [parameters] body))", which means the same thing. 

```
(defn my-addition [x y] (+ x y))
(my-addition 1 2)
```

## Some basic datatypes

### Symbols
So far we have seen two datatypes in our system: numbers like "1" and "2" and functions returned by "fn". Actually, we have seen another basic type: variable names used in "def" statements and "fn" definitions like "x" and "my-addition". This kind of object is called a *symbol* in LISP. When the Scheme interpreter sees a symbol it assumes this is a variable and it tries to look up the value for that variable. If the variable has not been bound to value, you will get an error.

```
some-symbol
```

What if we want to talk about the symbol itself, instead of always assuming that it is the name of a variable bound to some value? In this case, we can use the "quote" procedure. The quote procedure takes its argument and returns a *quoted* version of that argument. Quoted values are treated **as is** by the interpreter. That is, they are their own value. 

```
(quote some-symbol)
```

```
(def my-variable (quote some-symbol))
my-variable
```

In the expression above, we created a variable called "my-variable" and bound it to the value of the expression "(quote some-symbol)". We then asked Clojure to interpret the symbol "my-variable". The language assumed that the symbol "my-variable" was a variable, and looked up its value which, thanks to the quote, was the **symbol** "my-symbol". Since we frequently want to quote expressions, Scheme provides a shorthand for this. Any expression preceded by a single quote "'" is considered to be quoted in the language.

```
'some-symbol
```

```
(def my-variable 'some-symbol)
my-variable
```

### Strings

In addition to numbers, procedures, and symbols, LISP also has strings. A string is written ""some string"".

```
(def my-string "some string")
```

### Lists

We have actually already seen many examples of lists in our code above. In Clojure lists are written as a sequence of things appearing between parenthese "(v1 v2 v3 ...)". In other words, much of the code above consists of lists. In particular, combinations are just lists. When the Clojure gets a list as input, it assumes that this is a combination and tries to apply the function in the first position to the arguments in the rest of the positions (more on this later). We can explicitly construct a list using the "list" procedure.

```
(list 1 2 3)
```

A combination is just a list with a procedure in the first position.

```
(list (fn [x y] (+ x y)) 1 2)
```

The result of evaluating the expression above is a list with a procedure in the first position and the values "1" and "2" in the second and third position. This combination can be evaluated to produce an output.

```
(eval (list (fn [x y] (+ x y)) 1 2))
```

We can also quote a list to prevent the interpreter from treating it as a combination. 

```
'(1 2 3)
```

There is an important special case of lists in LISP which is usually written "'()". This is the empty list and is very important for reasons we will see below. We could also get the empty list by calling "list" with no arguments like this "(list)". 
```
'()
```

```
(list)
```