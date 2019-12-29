---
layout: post
title: "Deducing prime factors through elimination"
date: 2019-12-29T18:07:44+05:30
categories: [math]
tags: [Integers, Proof Techniques, Prime Numbers]
---

I recently found this interesting proof technique that uses a combination of deductive reasoning and integer factorization.
The prompt goes something like this: If $$ p $$ is prime and $$ k \in \mathbb{Z} $$ for which $$ 0 < k < p $$, then $$ p $$ divides $$ {p \choose k} $$.

Initially, there is a temptation to expand $$ { p \choose k } = \frac{p!}{k!(p-k)!} $$  to some expression $$ pa $$, where $$ a \in \mathbb{Z} $$.
This is natural given the goal of $$ p \; \vert { p \choose k } $$.
However, we soon realize that $$ p $$ being prime is not significant in this approach.
This should be enough to ward us off and look elsewhere.

At this point I gave up, only to find a nifty proof in the solutions:

1. Expand the usual $$ { p \choose k } = \frac{p!}{k!(p-k)!}$$
2. Manipulate it to the more interesting form $$ p! = { p \choose k } k! (p-k)! $$
3. Given that $$ p $$ is prime, it must present in the prime factorization of $$ p! $$
4. Due to the equality, $$ p $$ must then also be a factor of $$ { p \choose k } k! (p-k)! $$
5. Of the three terms, $$ k! $$ and $$ (p-k)! $$ are products of numbers smaller than $$ p $$ and therefore cannot contain the prime number $$ p $$ as their factors.
6. This leaves us with $$ { p \choose k } $$ as the only possible term with $$ p $$ in its factorization.
7. Therefore, $$ p $$ divides $$ { p \choose k } $$. $$ \Box $$

Some notes on the above approach:
* The critical part of the proof is where it uses deductive reasoning and comparison to isolate $$ { p \choose k } $$ as the only possible multiple of $$ p $$.
* The form $$ p! = { p \choose k } k! (p-k)! $$ is also interesting because it does not feature any nasty integer division.
This sidesteps the problem of having to prove that any intermediate fractions are integers and also makes way for prime factorization.
* It is a nice example of how prime factorization should be the first thing that comes to mind when discussing prime numbers.

The above problem is sourced from the fourth chapter of the excellent [Book of Proof](https://www.people.vcu.edu/~rhammack/BookOfProof/) by Richard Hammack.
