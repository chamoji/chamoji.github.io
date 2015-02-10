---
title: The Options Algorithm
layout: post
date: 2015-02-09
---

## Introduction ##
Any fan of Gradius should recognize the unique "Options"
mechanic that has become a staple of the series. Some of these fans
are also programmers, hobbyist or otherwise, that would like to mimic
this mechanic in their own creations (hint hint). I have done my own
research on this mechanic and have found very little in regards to
implementation and examples.

Enter: this tutorial.

## Tutorial Objective ##
In this tutorial I will describe my way of implementing the
Options snake-like behavior in a general way. I will briefly describe
an approach I took that failed initially. Then I finish off by
explaining my final implementation which is a culmination of what
worked from the previous failures.

My hope is that you do not just copy code and pray it works.
What I provide here is the intuition behind the development of this
algorithm. It's up to you to understand it and apply the concepts
explained here. For that reason I have very sparingly sprinkled some
pseudo-code to illustrate certain points.

## Options Algorithm Basics ##
For those unfamiliar with the concept of Options here is a
quick rundown of what they are all about.

Options are usually used in a STG (Shooting Game) context.
Whether it is a horizontal or vertical STG, an Option is the term
used to describe a supplemental fighter to the main ship or
character.

The Options I will go over this tutorial are the classic ones
which exhibit a snake-like behavior that trail behind the player's
character.

An algorithm that can accomplish this behavior will have the
following properties:

* Ways to retrieve the main ship's coordinates and store it.
* Ways to update the Options coordinates based on some rule.
* Only updates the positions when the player inputs a movement command.
* Follows the leader's path exactly but with some delay for each 
  additional follower.
 

## Attempt 1: Distance-Based Approach ##
Observe the following code which is executed during a movement
command (player has input left, right, up, or down):

	if (distance_from_leader > GAP_SIZE) {
		// get main ship's previous position
		// update the Options coordinates 
	}

This approach uses distance as an indicator of when to move the 
Options to the leader's previous coordinates. The gap size 
condition is a very explicit way of getting the Options separated.
Up to a certain point, this approach accomplishes trailing the 
leader well.


The problem with this implementation? 

_Distance is not a consistent enough factor to rely on._

The actual Options behavior keeps a constant distance away from the leader and 
a constant distance away among each of the Options.

Problem: A distance-based approach will cause drifting.

Depending on when you update the previous position of the leader, this will
result in a drifting effect. That is, as the main ship passes through the
Options, the position of the leader is temporarily unused.

Therefore, as long as:

	*distance_from_leader <= GAP_SIZE*

the Options will "drift" further and further away from the leader.

So in order to continue we need to solve this problem along the way. But don't 
fret. At the very least we have a part of the algorithm solved. That is, we 
have a way of making the options follow the leader so it's a start. Keeping
track of some size of the path seemed to be working, it just needs something 
simpler to accomplish the task.

## Attempt 2: Queue-Based Approach ##
So knowing that distance wasn't the way to go I had to search
through other avenues. Eventually I arrived at a very basic data
structure. 

The queue...

A queue is the perfect data structure for the job. Its FIFO
(First-in-first-out) property fits like a glove with the Options
behavior. A global queue can be used to store the Options' positions
so that as they get in line you can grab the previous element's
position and the newest element in line can follow the correct
element in the queue. Additionally, you can use a queue to store the
path each element will take (a queue for the next person in line's
previous position) so that each Option follows the correct "person"
in line.

So a typical scenario would be like the following:

Option#1 gets in line. It gets the leader's position 
and stores it in its own queue. Then it stores its own 
position in a global queue that all elements can see. 
This sets up the global queue for additional elements so 
that they can grab the previous element's position. The next person 
in line can now follow the previous person in line.

So now this leaves us with the same problem. When do we update the
positions of each element in the queue if distance will cause
drifting? The answer is to use a consistent factor to get consistent
results. Looking at our setup we see that we are _constantly_ adding and
removing elements from our queues. As the queues grow, so does the path each
element has to follow and vice versa. So it's only natural that we come to our
answer.

Solution: The path queue offers a reliable figure such that using it as our
basis for updating the positions of each element will be consistent. A path
queue's size solves our problem.

## And Finally... ##
We come to a general algorithm we can apply in any language to
get the snake-like behavior of the classic Options of Gradius fame.
The only thing new we need to add is a factor called a delay or a
step-size. This figure determines at what size we should start
letting the elements follow their paths. A size of, say, 20 will tell
each Option to follow their path after 20 positions have been filled
in their path queues.

In the main game loop:

	if (playerMoved) { 
		for (options : globalOptionsQueue) { 
			moveOptions();
		}
	}

moveOptions() function:

	if (isFirstOption) {
		updatePath(leaderPosition);
	} 
	else {
		updatePath(previousOptionPosition));
	}

	if (pathSize > pathDelay) {
		myX = headOfPathQueueX;
		myY = headOfPathQueueY;
		removeHeadOfQueue();
		updateGlobalOptionsQueue();
	}

So there you have it. The thought process behind my implementation of the
Options Algorithm.  

Last updated: February 9, 2015 by chamoji
