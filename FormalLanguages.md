---
title: Formal Languages
---

# The Problem: Beginnings

The goal of modern generative linguistics is to achieve a precise computational understanding of how language works. How do speakers turn the meanings they wish to communicate into utterances that can be spoken, written, or signed and how do listeners map these incoming signals to the meanings that they understand? Clearly, this is a big question whose answer will involve many components from understand the basic perceptual systems of the human mind to understanding what meaning is in the first place. Like all complex scientific problems, we need to make some simplifying assumptions in order to make progress. 

Let's start by making a few remarks about the part of the problem we will deal with in this course. Our first simplifying assumption is that we will focus on just the problem of explaining the structure of sentences. Consider the following English sentence.

> John loves Mary.

What can we say about a sentence like this? First, it is obviously built from a set of basic units like *words* and *morphemes*. Second, sentences are *compositional*: the meaning of the whole sentence is the result of the meaning of the individual words used in the sentence as well as the way they are combined. For example,

> Mary loves John.

means something quite different from the first sentence. As English speakers, we know something which tells us that the ordering of the words affects their combined meaning in systematic and predictable ways. Furthermore, many combinations of words are not valid in English.

> $$^*$$loves Mary John.

Note here we are using the English convention of using the symbol $$^*$$ at the beginning of a sequence that is not a possible English sentence or in technical terms is *ungrammatical*. While we may be able to guess what the speaker intended (or maybe not) if we heard this sequence of words, we know that it isn't valid English. Chomsky gave the following famous pair of examples which illustrates this point more forcefully. 

> Colorless green ideas sleep furiously.  
> $$^*$$Furiously green sleep ideas colorless. 

In the preceding examples, the first sentence is well-formed in English, while the second is not. What is striking is that the well-formedness of the first sentence doesn't seem to mean anything that makes any sense. Chomsky used this example to illustrate the point that whatever principles tell us what a possible English sentence is, they must be at least partially independent of whether or not the sequence has a meaning. Another famous example comes from Lewis Carrol's poem *Jabberwocky* which begins. 

> Twas bryllyg, and the slythy toves  
> Did gyre and gymble in the wabe:  
> All mimsy were the borogoves;  
> And the mome raths outgrabe.

These examples seem to suggest that we might make a start of our study of sentence structure by asking which sequences of words are possible, *grammatical* English sentences and which are not. This question of *grammaticality* is one of the central problems of natural language *syntax*&mdash;the scientific study of the grammar of sentences.

Before moving on, it is worth making a few comments on the study of grammatical and ungrammatical word sequences since it often leads to confusion. Our focus on th problem of grammatical and ungrammatical sequences is an idealization. The examples above suggest that we may be able say something useful about sentence structure without considering meaning. This isn't to suggest that meaning is not important: Everyone agrees that the ultimate problem we wish to solve is to understand how to map from form to meaning and back again. Considerations of meaning are central to the study of syntax, and we will bring them into play very shortly in this course. We start, however, with this simplified problem in the hope that it will teach us some lessons which will continue to be important as we develop more sophisticated models and consider more sophisticated kinds of data.


# Lexica and Strings

To begin our idealization, let's assume (incorrectly) that we have a fixed set of words in our language. We will write this set of words $$V$$ which stands for the set of words in our language or the *vocabulary*, sometimes this is called the *lexicon*&mdash;the technical term linguists use for the inventory of words (or morphemes) in a language. In formal language theory, this is primitive set of symbols is often also called the *alphabet* and is typically written $$\Sigma$$. But, since we are focused on sentence structure in this course we will use the term *vocabulary* and the symbol $$V$$ for this 
set. As an example, we might have a small vocabulary only consisting of the three words *John*, *loves* and *mary*, that is, $$V = \{John, loves, Mary\}$$. From a formal perspective, we don't usually care much about the actual members of $$V$$. In  formal examples we will often use simply symbols like $$a$$,$$b$$ instead of real words. We will insist for now, however, that the vocabulary is *finite*. 

<!-- todo: what is the best notation and terminology to use for \Sigma and strings and whatnot -->

To begin studying possible and impossible sentences, we will need some notion of a sequence of words. In formal language theory, this is called a *string* and is any *finite* sequence of symbols in $$W$$. For simplicity, let $$V = \{a,b\}$$. Note that we will use square brackets to indicate strings. Some strings *over* this lexicon (or alphabet) are $$[a]$$, $$[aaaab]$$, $$[ababababa]$$, etc. One reason we use brackets to indicate strings is so as not to confuse a string $$[a]$$ with a single symbol from the symbol itself $$a$$. We will sometimes use variable $$x, y, z, ...$$ to refer to strings over the vocabulary $$V$$. 

The *length* of a string $$|x|$$ is the number of symbols in the string. For example, $$|[aba]|=3$$.

There is a special, unique string called the *null string* that has length $$0$$ and is written $$[]$$, i.e., $$|[]|=0$$. In traditional notation, the null string is usually written $$\epsilon$$, but our notation makes its properties clearer. This string always exists over any lexicon. 

<!-- todo: write the length function recursively -->

Let $$[V]$$ be the set of shortest strings that includes the vocabulary and the null string. In other words if $$V=\{a,b\}$$ then $$[V]=\{[],[a],[b]\}$$. Essentially, putting brackets around the vocabulary just "wraps" each elementary symbols into a string and adds the empty string.
The set of all possible strings over a vocabulary $$V$$ is written $$[V]^*$$, a symbol called the *Kleene star*. Thus, $$[V]^*=[\{a\}]^*=\{[],[a],[aa],[aaa],[aaaa],...\}$$ and $$[V]^*=[\{a,b\}]^*=\{[],[a],[b],[ab],[ba],[aaa],[bbb],[aba],[bba],[abb],...\}$$. If we are using real words or other symbols of length longer than $$1$$, we will put spaces in to indicate the elements of the string, e.g., $$[John\ loves\ Mary]$$.

<!-- todo: what is the cardinality of W^* -->

When talking about sets of strings, we will take the empty set $$\emptyset$$ to contain the null string, that is, $$\emptyset=\{[]\}$$.

The basic operation that we can perform on strings is *concatenation*. If we have two string variables $$x$$ and $$y$$ we write the concatenation like $$x \cdot y$$, or sometimes just $$xy$$. If we are talking some actual strings $$[ab]$$ and $$[ba]$$ we will write $$[ab]\cdot[ba]=[abba]$$.

Concatenation is associative, which means it doesn't matter what order you do it in, i.e., $$(xy)z=x(yz)$$, and the null string is an *identity* for the operation which means concatenating the empty string on anything gives you back the empty string  $$x \cdot []=[] \cdot x=x$$. The length of a concatenated pair of string is the sum of the lengths of each $$|xy|=|x|+|y|$$.

We write $$x^n$$ for $$n$$ concatenations of the string $$x$$. So if $$x=[ab]$$, $$x^3=[ababab]$$, $$x^1=[ab]$$, and $$x^0=[]$$.

A *prefix* of a string $$x$$ is an initial substring of $$x$$. For instance, the string $$[ab]$$ is a prefix of the string $$[abababab]$$. Note that we consider the empty string a prefix of every other string and every string is a prefix of itself.


## Representing Formal Strings

We have now defined a simple idealization of a sentence as a *string* of words (or symbols). How can we represent this in LISP? In this course, we will use *symbols* to represent the atomic symbols in $$V$$. As our notation has hopefully made clear, a natural representation for formal strings is the *list* datatype. 

```
(def my-string '(a b a b))
my-string
```

## Concatenation

We have already seen how we can build up lists by using "cons" together with the null string "'()". When using `cons` to build a string of symbols, we pass in two arguments: a symbol and another string.

```
(cons 'a my-string)
```
