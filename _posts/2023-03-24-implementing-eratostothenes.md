---
title: Implementing the Sieve of Eratosthenes
layout: post
---

I was inspired by [this](https://codeforces.com/blog/entry/54090) tutorial to try my hand at a bit of mathematics in Python. The article was very helpful on explaining the basics of sieves to generate prime numbers, but the language used (probably C or C++) was unfamiliar to me, so I wanted to rewrite the same thing with Python. Here was my implementation of the basic sieve:

``` python
def sieve (n):
	composites = [False for n in range(n)]
	primes = []
	for num, bool_val in  enumerate(composites):
		if num != 0 and num != 1:
			if bool_val is False:
				primes.append(num) 
				for multiples in range (num,n,num):
					composites[multiples] = True
	return primes
```

The basic idea of the function is to create an array of boolean values that represent whether the number at the `index` is composite -- `True` for a composite number, `False` for a prime. Using this line of code, we generate the required array, letting each number be false until proven guilty -- or rather, I suppose, assumed prime until proven composite:

``` python
composites = [False for n in range(n)]
```

We also initialize a seperate array that will hold our primes. Now, the original program implements the loops with traditional `for` syntax. While this can be done, the more Pythonic way of pursuing the issue is considered to be the `enumerate()` function, which will allow us to keep track of the separate boolean values as well as their numerical index.

The first `if` lets us skip indices 0 and 1, which are obviously not numbers we want to work with here! We then say that if the boolean is `False` -- that is, we've found one of our primes -- we want to generate all the multiples of the primes under our limit and set the values at those indices to `True`, meaning we know them to be multiples of a prime number and hence composites. Keep in mind that the third argument to the `range()` function is an interval -- so `range(num,n,num)` asks for all the multiples of `num` up to our limit, the argument `n`. 

Lastly, we return our array of primes. If I run this function with a limit of `5000`, I get all my primes in 59ms. But just as the linked article says, we can improve the efficiency by creating a linear sieve:

``` python
def linear_sieve(n):
	composites = [False for n in range(n)]
	primes = []
	for num, bool_val in  enumerate(composites):
		if num != 0 and num != 1:
			if bool_val is False:
				primes.append(num) 
			for p in primes:
				if (p*num<len(composites)):
					composites[p*num] = True
                else: # this should be under the p in primes loop, but MarkDown doesn't like that
                    break
				if (num%p == 0):
					break
	return primes
```

Now this certainly _sounds_ like it should require fewer calculations per loop, and hence be much faster. After all, instead of running through every multiple each time, we're only adding a few multiples at a time. But in fact my computer runs `linear_sieve()` in 61ms, a negligible difference that seems to grow exponentially with larger numbers! Apparently, this is a [known issue](https://programmingpraxis.com/2012/01/06/pritchards-wheel-sieve/) and involves the types of calculations needed for the linear sieve rather than simply the total number of calculations (if all calculations could be performed in an equal amount of time, the linear sieve would be more efficient, but in practice computers perform addition-based calculations quicker than others).

I did, bowever, implement one optimzation suggested [elsewhere](https://www.cs.hmc.edu/~oneill/papers/Sieve-JFP.pdf), which was substituting `range(num*num,n,num)` for `range (num,n,num)` -- that did, in fact, make the standard sieve much faster. Of course, in addition to practical problems with the linear sieve, it's entirely possible that my implementation was faulty in some significant way, about which comments and corrections would be very welcome.