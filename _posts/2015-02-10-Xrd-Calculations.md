---
title: Xrd Statistics
layout: post
date: 2015-02-10
---

Let's do some math.

Xrd recognizes 9 different directional inputs:

* Neutral (5)
* Left (4)
* Right (6)
* Up (8)
* Down (2)
* Up-Left (7)
* Up-Right (9)
* Down-Left (1)
* Down-Right (3)

For buttons, Xrd recognizes 6 inputs:

* Punch (P)
* Kick (K)
* Slash (S)
* H-Slash (H)
* Dust (D)
* Taunt (T)

	How many different combinations of _Direction_ + _Button_ exist?
	In other words, how many single direction "moves" are there?

For example, 6H is a single direction move whereas 623H is not.

## Enumerating the combinations ##

To figure this out, we need to know which figures to add to get the result we want.

A single direction move is simply selecting a number from 1-9 and combining it with
the number of different button combinations possible given 6 inputs.

	Total Combinations of Single-Direction Moves = (Number of directions) * (Button Combination)

	Number of directions = 9 choose 1
	Number of directions = 9

	Number of Button Combinations = (6 choose 1) + (6 choose 2) + ... + (6 choose 6)
	Number of Button Combinations = 6 + 15 + 20 + 15 + 6 + 1 = 63

	9 * 63 = 567 total single-directional moves

So this means there are 567 different ways to input one direction (1-9) 
with any combination of the 6 buttons (P, P+K, P+K+S, ... , P+K+S+H+D+T).

But, for actual application's sake, let's ignore the number of combinations that include the 
Taunt button.

If we ignore the Taunt button, we have...

	9 * [ (5 choose 1) + (5 choose 2) + ... + (5 choose 5) ]
	9 * 31
	279 single-directional moves (excluding Taunt button)

Interesting.

Ok, math time is over. See you next time.


