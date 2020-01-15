---
layout: post
title: "Spotting Consecutive Integers"
date: 2020-01-15T13:01:30+05:30
categories: [math]
tags: [Integers, Proof Techniques]
---

A useful technique that stumped me on a couple of proofs recently was the idea of "consecutive integers".
A friend had the following proposition: The result of subtracting a number from its cube is divisible by $$ 3 $$.

We can also state the problem in symbols: for any $$ a \in \mathbb{Z} $$, it is true that $$ 3 \vert (a^3 - a) $$.
To quickly check if this makes sense, we also write down the following examples:

$$ -2^3 - (-2) = -6 = 3 \cdot -2 $$

$$ -1^3 - (-1) = 0 = 3 \cdot 0 $$

$$ 0^3 - 0 = 0 = 3 \cdot 0 $$

$$ 1^3 - 1 = 0 = 3 \cdot 0 $$

$$ 2^3 - 2 = 6 = 3 \cdot 2 $$

$$ 3^3 - 3 = 24 = 3 \cdot 8 $$

$$ 4^3 - 4 = 60 = 3 \cdot 20 $$

We can use the idea that $$ (a^3 - a) $$ is divisible by $$ 3 $$, if it is equal to $$ 3 \cdot b $$ where $$ b \in \mathbb{Z} $$.

_Proof._ Suppose $$ a \in \mathbb{Z} $$. We start with $$ a^3 - a $$. \
Pulling out $$ a $$, we get $$ a ( a^2 - 1) $$. \
The next step is to spot the difference of squares: $$ a ( a^2 - 1^2) = a (a - 1) (a + 1)$$. \

At this point we get stuck, as there is not much left to do arithmetically.
We still don't have the $$ 3 $$ or the $$ b $$ we're looking for.

However, there are some hints to help us.
The first thing to note is that we have _three_ terms: $$ a, ( a - 1), ( a + 1) $$.
We can further re-arrange these to get: $$ ( a - 1)(a + 0)( a + 1) $$.
These are __three consecutive integers__.

Given $$ n $$ consecutive integers, we can be sure that exactly one of those integers is divisible by $$ n $$.
Thus exactly one of $$ \{ (a-1), (a+0), (a+1) \} $$ is divisible by $$ 3 $$.
Which means that we can write the expression in three possible cases, where $$ c \in \mathbb{Z} $$:

$$ (3c) (a + 0) (a + 1) $$

$$ (a - 1) (3c) (a + 1) $$

$$ (a - 1) (a + 0) (3c) $$

For each of these cases, it is trivial to extract $$ b \in \mathbb{Z} $$ such that the expression becomes $$ 3 b $$.

$$ (3c) (a + 0) (a + 1) = 3b $$, where $$ b = c (a + 0) (a + 1) $$

$$ (a - 1) (3c) (a + 1) = 3b $$, where $$ b = (a - 1) c (a + 1) $$

$$ (a - 1) (a + 0) (3c) = 3b $$, where $$ b = (a - 1) (a + 0) c $$

For the three forms of $$ (a^3 - a) $$, there is a $$ b $$ such that $$ (a^3 - a) = 3b $$. \
Therefore, $$ (a^3 -3) $$ is divisible by $$ 3 $$. $$ \Box $$

Here is another problem that relies on a similar appearance of consecutive integers.
It can be found in the fifth chapter of the amazing [Book of Proof](https://www.people.vcu.edu/~rhammack/BookOfProof/).

If $$ n $$ is odd, then $$ 8 \vert (n^2 - 1) $$.
We will of course try to show that $$ n^2 -1 $$ is equal to $$ 8c $$ where $$ c \in \mathbb{Z} $$.

_Proof._ Suppose $$ n $$ is odd.
We can write $$ n = 2a + 1 $$, for some $$ a \in \mathbb{Z} $$.
The expression $$ n^2 - 1 $$ can be simplified as:

$$ n^2 -1 = (2a + 1)^2 - 1 = 4a^2 + 4a = 4a(a + 1) $$

Again we get stuck arithmetically, the required '$$ 8 $$' is nowhere to be found in $$ 4a(a+1) $$ .
The hint lies in the possibility that we need to pull out a '$$ 2 $$' from somewhere such that the '$$ 4 $$' can be written as an '$$ 8 $$'.
On careful observation, we notice that the two terms $$ a $$ and $$ (a + 1) $$ are consecutive integers.
Therefore, exactly one of those must be divisible by $$ 2 $$.
This leads to two cases, where $$ b \in \mathbb{Z} $$:

$$ 4 (2b) (a+1) $$

$$ 4 (a) (2b) $$

In either case, we can extract a $$ c \in \mathbb{Z} $$ such that:

$$ 4 (2b) (a+1) = 8 b (a+1) = 8c $$, where $$ c = b(a+1)$$

$$ 4 (a) (2b) = 8 ab  = 8c $$, where $$ c = ab $$

Here too, the two forms for $$ (n^2 - 1) $$ are equal to $$ 8c $$. \
Therefore, $$ (n^2 -1) $$ is divisible by $$ 8 $$. $$ \Box $$
