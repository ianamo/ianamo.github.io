---
title: A Regular Expression for Primes
layout: post
---

Apologies for not updating this blog for some time, but be sure to check out this article about using a regular expression to [test for prime numbers](https://www.noulakaz.net/2007/03/18/a-regular-expression-to-check-for-prime-numbers/). The way that this regular expression turns a number into a kind of typographic expression, and then uses what is essentially a typographic test to express a mathematical truth, reminded me a lot of the system TNT that Douglas Hofstadter works out in _Godel, Escher, Bach_. 

One wonders what other mathematical expressions might be susceptible to this kind of treatment. I've been revisiting one of my favorite websites, [Project Euler](https://projecteuler.net/), and returning to a problem that for most people would probably be embarassingly easy, but which has stumped me for some time, about Pythagorean triples. Pythagorean triples, of course, are those integers that we find in sides of right-angled triangles, that follow the famous pattern of `a^2 + b^2 = c^2`, or `a**2 + b**2 == c**2`, to put it in a syntax that looks more like code. Most famously, of course, the numbers 3, 4, 5 are a Pythagorean triple. 

One interesting thing to notice here is just that there's a curious satisfaction that comes from finding these kinds of parallels, whether in a typographic test that expresses a mathematical truth or a geometric figure that expresses a mathematic truth. The satisfaction seems to derive from a sort of surprise, as though it weren't obvious that such parallels should exist between different kinds of formal systems. Moreover, the expression of the "same" truth in multiple formats seems to permit a fuller expression and understanding, as though each new instantiation of the same truth revealed a different facet of what the truth was in fact. (Indeed, simply calling it the "same" truth seems to implicate us in all kinds of interesting Platonic questions about the nature of truth as a whole.)

So, 3, 4, and 5 are a Pythagorean triple, and they sum to 12. Would there be a way, beginning from 12, to test whether 12 could be broken apart into a Pythagorean triple? So that we begin with, say:

```
$$$$$$$$$$$$
```

and by some typographical algorithm end up with:

```
$$$ + $$$$ + $$$$$
```

It seems like something like this should be possible. After all, to say that these can be the length in integers of the sides of a right-angled triangle is to say that, visually, we can begin at a point, "march" left for three units, march upwards for four units, and then march back to the origin in five units. Surely, then, there must be other kinds of regularity to the pattern that a regex could capture in a way that would be analogous to the test for primes. 

Now, in Euclid's geometric version, we might say this: can this single number 12 be divided in such a way that, in three parts, two parts can be the sides of squares and still leave enough "room" for the last line to be squared with an area equal to the other two squares? 