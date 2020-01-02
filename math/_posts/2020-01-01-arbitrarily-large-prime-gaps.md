---
layout: post
title: "Arbitrarily Large Prime Gaps"
date: 2020-01-01T18:37:25+05:30
categories: [math]
tags: [Integers, Proof Techniques, Prime Numbers]
---

If $$ n \in \mathbb{N} $$ and $$ n \geq 2 $$, then the numbers $$ [n! + 2, n! + 3, n! + 4, \ldots , n! + n] $$ are all composite.
Thus for any $$ n \geq 2 $$, we can find $$ n - 1 $$ consecutive composite numbers.
The implication here being that there are arbitrarily large "gaps" between prime numbers.

I came up with an arithmetic proof which utilizes the fact that any composite number $$ c $$ can be written as $$ c = ab $$ where $$ a,b \in \mathbb{N} $$ and $$ 1 < a,b < c $$.

_Proof._ Assume $$ C $$ is the set of all consecutive numbers following $$ n! + 1 $$ such that:

$$ C = \{ n! + a : a \in \mathbb{N} \text{ and } 1 < a \leq n \} $$

For any $$ c \in C $$ we can write:

$$ c = n! + a = a ( \frac{n!}{a} + 1 ) = ab \text{, where } b = \frac{n!}{a} + 1 $$

We already know that $$ a \in \mathbb{N} $$ and $$ 1 < a \leq n < c $$.
All that remains is to show that $$ b \in \mathbb{N} $$ and $$ 1 < b < c $$:

* $$ b = (\frac{n!}{a} + 1) \in \mathbb{N} $$ because $$ a \leq n \implies a \vert n!$$
* $$ ab = c $$ and $$ 1 < a < c$$, therefore $$ 1 < b < c $$

Therefore any $$ c \in C $$ is composite. $$ \Box $$

I realized that I took the bumpy route when I read the wikipedia article on [Prime Gaps](https://en.wikipedia.org/wiki/Prime_gap#Simple_observations), which has a much simpler proof.

_Proof._ In the sequence $$ [n! + 2, n! + 3, n! + 4, \ldots , n! + n] $$ the first term is divisible by $$ 2 $$, the second term by $$ 3 $$ and so on. Thus this is a sequence of $$ n - 1 $$ consecutive composite integers. $$ \Box $$

This one-liner works because all numbers from $$ 1 \ldots n $$ are divisors of $$ n! $$ 🤦🏽‍♂️
