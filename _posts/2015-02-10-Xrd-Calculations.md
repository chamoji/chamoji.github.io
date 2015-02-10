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

Another way of asking this question is, at any given frame, how many possible
inputs does the game recognize?


## Enumerating the combinations ##

To figure this out, we need to know which figures to add to get the result
we want.

A single direction move is simply selecting a number from 1-9 and combining it 
with the number of different button combinations possible given 6 inputs. 

A single direction move also consists of only a directional input 
with no button input attached.

### Total Combinations of Single-Direction Moves ###

For _d_ directions and _b_ button-inputs, the total number of combinations _I_
is given by the following equation:

<img src="/assets/total_inputs.png"/>

So this means there are 576 different ways to input one direction
with any combination of the 6 buttons.

So if you are aiming for only one specific input out of the 288 possible 
(excluding taunt)...

	1/288 = ~0.35%

But, this isn't the whole story. 

In a match, the dynamics of the fight changes which inputs you 
actually want to come out. 

In other words, which inputs actually result in some action differs over time.

For example, during blockstun you are limited to a certain subset of the total
moves (continue to guard with 1 or 4, and then Dead Angle with 6P+K).

So, how many ways are there to input burst?
Let's also include overlapping inputs for RC and IK Activation in the total.

	135 different ways to input burst.

	135/288 	
	= 46.875% of total possible inputs

Given that a round lasts 99 seconds and that Xrd runs on 60 frames per second: 

	99 seconds * 60 frames per second
	= 5940 frames 

This is assuming things like hitstop, superflash, or time slowing effects do
not add additional frames by momentarily stopping the clock.

What does all of this mean?

I don't know. I just wanted to do some math.
See you next time.
