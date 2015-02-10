---
title: Xrd Statistics
layout: post
date: 2015-02-10
---

I think it's interesting to think about games in a different way.

_Forget tier lists._

Instead, let's do some math on some more general mechanics...

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

Another way of asking this question is, at any given frame, how many possible inputs
does the game recognize?


## Enumerating the combinations ##

To figure this out, we need to know which figures to add to get the result we want.

A single direction move is simply selecting a number from 1-9 and combining it with
the number of different button combinations possible given 6 inputs. A single direction move
also consists of only a directional input with no button input attached.

	Total Combinations of Single-Direction Moves =
	(Number of directions) * (Button Combination) + (Number of directions)

	Number of directions = 9 choose 1
	Number of directions = 9

	Number of Button Combinations = (6 choose 1) + (6 choose 2) + ... + (6 choose 6)
	Number of Button Combinations = 6 + 15 + 20 + 15 + 6 + 1 = 63

	9 * 63 = 567 total button combinations with direction

	Total Single-Direction moves = 567 + 9 = 576

So this means there are 576 different ways to input one direction (1-9) 
with any combination of the 6 buttons (P, P+K, P+K+S, ... , P+K+S+H+D+T).

But, for actual application's sake, let's ignore the number of combinations that include the 
Taunt button.

If we ignore the Taunt button, we have...

	9 * [ (5 choose 1) + (5 choose 2) + ... + (5 choose 5) ]
	9 * 31 = 279
	279 + 9 * (5 choose 0) = 
	288 single-directional moves (excluding Taunt button)

Interesting.

So if you are truly aiming for only 1 input out of the 288 possible (excluding taunt).
1/288 = ~0.35%

But, this isn't the whole story. In a match the dynamics of the fight change which inputs you actually
want to come out. In other words, which inputs actually result in some action differs over time.
For example, during blockstun you are limited to a certain subset of the total moves (continue to
guard with 1 or 4, and then Dead Angle with 6P+K).

With those facts in mind, we can come up with a list of percentages regarding different inputs:

	How many ways to input burst (including overlapping inputs for RC and IK Activate)?
	Answer: 135 different ways to burst. 135/288 = 46.875%


Ok, math time is over. See you next time.

