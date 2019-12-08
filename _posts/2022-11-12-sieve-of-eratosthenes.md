---
title: "Sieve of Eratosthenes"
tags: algorithm math
---


## Finding primes up to n

Finding primes with a computer is perhaps one of the first few steps that a programmer learns. Most people would go about finding primes with a brute force type method. For instance, given a number 13, the beginner would resort to checking divisibility for numbers 1,2,3, ... up to 12. This is no doubt a correct method, and for the number 13, your computer would compute without breaking a sweat. However, you will find your computer would a very very long time when you look at much larger numbers.

## Code

Here is a simple code in GAP that generates the number of primes (This is deprecated code. I have not used GAP in years)

`
primes:= [];;
numbers:= [2..1000];;
for p in numbers do
    Add(primes, p); #adding p to list
    for n in numbers do
        if n mod p = 0 then
            Unbind(numbers[n]); #removing p from list
        fi;
    od;
od;
`

`
include code for javascript here
`


## Small Computational Trick

There are a few computational tricks, which are useful like sqrt(n), but the best way is to look at the SIEVE OF ERATOSTHENES.

However, the main problem here is that how a person structures his or her code, will be different. So I will explain the theory first and then the code.

So the theory states, if you find a small prime i.e, 2 then you can be sure that anything that is a multiple of that small prime is not a prime. So in the case of 2,instead of having 98 numbers to check, we have only 49 numbers to check whether are prime or not. And we reduce that by further removing any multiples of 3, and so would only have roughly 49/3 numbers to check and so on.

From now on, I will just be talking code Jargon. Note: If any are curious, I am using GAP language.
In the outer loop, I am adding the n's from the numbers list into my prime list one-by-one. In the inner loop, if n is divisible by the any prime in my prime list, then it is taken out using the unbind command. So the concept is that I eliminate the numbers in which I can put inside, so I have to put in less.

