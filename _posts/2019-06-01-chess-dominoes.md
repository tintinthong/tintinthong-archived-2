---
title: "Chess Dominoes"
tags: puzzle
---


<p>
  <!-- <a href="MY WEBSITE LINK" target="_blank"> -->
    <img src="/img/chess.jpg" style='width:60%; display:block; margin-left:auto;margin-right:auto' border="0" alt="Null">
  <!-- </a> -->
</p>

## Question 

A normal chessboard has 64 squares. Say if I have a rectangular tile (2 by 1), it is obvious that I can fit 64 tiles onto the chessboard exactly. Consider now that I removed the two corner pieces highlighted in red. Will I be able to fit 62 square tiles exactly?

## My Thoughts

This is perhaps one of my favorite puzzles because of the simplicity in it's solution. But first let's go through my thought process.

The first thing I tried is to start placing (2 by 1) pieces. 1st try: Doesn't seem to fit. 2nd try: Attempt different orientation strategy, still don't fit. As most puzzles, my gut tells me that brute force is almost never the solution. 

Then I try simplifying the problem: 8x8 should be equivalent to 4 x 4 or 2 x 2. But, if I removed the corner pieces for 2 x 2 I am left with a solution which is impossible -- 2 x 2 is impossible. Perhaps, I can use some form of induction. If a base case is true (2 x 2) and I can prove that every nxn case implies (n + 1)x(n + 1) case, then 8 x 8 (the original chess board) would just be an instance of the induction. Let's list out some move. 3 x 3 is impossible too because I would have an odd number of tiles to fill which is 9-2=7. It is obvious that a (2 by 1) tile can't fit exactly. 4x4 seems quite impossible too after some iterations of trying. 

Can the induction chain of impossibilities still work. Well, odd x odd breaks the chain, so if I were to do an induction it would have to go for even sequences only, i.e. (2n) x (2n). But, how do I do the general case of (2n) x (2n) to (2n+1) x (2n+1). So I try  to count the pieces on the board to see that maybe there will be something like an odd difference -- obviously odd. FAIL FAIL FAIL. I'm stuck. Please help me. 

I did, however, start making observations. For example, if I chose the complementary corner pieces, the problem is isomorphic by rotation. What if I chose a (2 by 1) piece randomly in the middle of the board. The (2 by 1) pieces fit because there is an even row, unless the (2 by 1) piece leaves an odd number on the left and an odd number on the right. However, still no solution.

## Solution
It took me about 20 minutes before I saw it. AHA! EUREKA! Can you see it? The idea is to observe the color of the tiles. We need count the color of the tiles. As the board is chequered, the corner pieces are of the same color. Meaning that there will be 8 x 8=64-2= 62 = 30 white + 32 black. But, a (2 by 1) piece will have 1 white and 1 black. A 62 tile board that is made out of (2 by 1) tiles would have the same amount of white and black tiles, i.e. 31 white and 31 black. 
It appars tht we were missing the context of the problem. My mistake was to jump to brute-force and induction; these were methods I was familiar with. It would have been helpful if I was more sensitive to the nature of the chessboard (puzzle). 

Wouldn't you argree that the problem will be a lot harder if we did not see a chessboard, but a white gride of 62 tiles. We would have to solve it by coloring. 

Further questions I would consider is: 

1. Does this apply to (2n x 2n). Yes, since opposite corners will always be the same color.

2. We solved this for (even x even). Is there an equivalent problem for (odd x odd)? Perhaps, if we removed 3 tiles from an odd by odd. We would have one added complexity. We can choose (black white black) and a (white black white). Try to code this out?
3. Rubix cube ;).
This i an ineresting problem, which  brings to mind the idea of coloring to reveal alternating patterns in our puzzle. I learnt that jumping head first with the method you are familiar with might not be wise. Instead, one has to be sensitive to the nature of the problem. Play around with the structure and try to invent plausible mind tools of solving.



