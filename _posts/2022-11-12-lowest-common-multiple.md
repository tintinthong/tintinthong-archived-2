---
# layout: post
title: "Lowest Common Multiple"
# date: 2017-11-12
# comments: true
description: "Imrproving a simple algorithm (speed)"
tags: algorithm
---

> 2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder. What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?

I had a lot of difficulty with Euler Problem 5. A rather simple problem which I found particularly difficult. Below is some Python code to solve this problem: 

<pre><code> 

i = 1
for k in (range(1, 21)):
  if i % k > 0:
    for j in range(1, 21):
      if (i*j) % k == 0:
        i *= j
        break
print i

</code></pre>
