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
