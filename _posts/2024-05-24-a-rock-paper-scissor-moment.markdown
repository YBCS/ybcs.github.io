---
layout: post
title:  "A Rock Paper Scissor Moment!"
date:   2024-05-24 00:35:45 +0530
categories: tech blog
---
Welcome to my first blog

Goals:
  - non technical people should be able to understand
  - it should be slightly interactive
    - play/pause
    - debug view
  - It should have some humour
  - should have some code
  - mention that tweet which inspired this project
  - Should contain "additional resources" 
  - should contain "further work"


Back in 2022, I saw a tweet about a rock paper scissors simulation. Randomly moving sprites of rock, paper and scissors in the screen and based on the classic rules,they would transform from one form to another when they touch. 

It was a viral tweet and I wanted to recreate it. At that time I knew very little about game development and computer graphics and I was not motivated enough to carry the project through. Fast forward to today, I've learned sufficient methodologies to make the project a reality. 
So I did it. This blog covers what it takes to recreate this.

### The Original Tweet: 

---

<!-- <iframe style="border: 0px; width: 600px; height: 600px;" src="https://editor.p5js.org/ybcs/full/f5AdX-O1t">
</iframe> -->


<blockquote class="twitter-tweet"><p lang="en" dir="ltr">sorry i can’t come tonight, i’m watching the rock paper scissors simulator season finale <a href="https://t.co/n4l5xZtVHV">pic.twitter.com/n4l5xZtVHV</a></p>&mdash; juan (@juanbuis) <a href="https://twitter.com/juanbuis/status/1600155605112496129?ref_src=twsrc%5Etfw">December 6, 2022</a></blockquote> 
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

---

If you're 90's kid, do you remember that floating dvd icon which moves around the screen and bounces off of the edges. wot

I thought making that would be very easy. hmmm...




{% highlight javascript %}
class Agent {

}
{% endhighlight %}




Analysis: 
At a glance this is what I notice about the game.

The r p s let's call it an agent, moves in random direction, tries to convert other weaker agent to itself (here weaker means by the rules). Agent does not go out of boundary. The game stops when all the agents are converted to the same 'type' and that 'type'  becomes winner.

Simple I thought. 

Hahahah lol 

I had not done much simulation work in the past, most of my knowledge is on building web based management tool. So naturally I underestimated the requirements. Classic. 

I started with a base prototype. Straight movements and simple boundary checking. My plan was to draw a rectangle and have it move around the canvas and bounce off it's boundaries. It should look like that bouncing dvd animation we all saw as a kid! 

To make my life easier, I picked up p5js a library to aid me in animation.... Drawing a box is simple, there's a rect function.Having it move across the screen can be done by giving it a position and incrementing it's coordinates every frame of the animation. 
I checked it's boundary like this 
It reads, if x position is below 0 or x is above width then x is out of bounds. We can make it change direction every time it goes out of bounds. We do the same thing for y position. 
It looks like this 

Now we can look at many rectangles at a time. This was my first fumble, I didn't realise the kind of work it would take for "collision detection" (there are entire books on this topic lol). 
A naive way to do this is for every agent we check every other agent and see if we are intersecting/colliding/overlapping.
Well for 10 items it needs 10*10 = 100 comparison
And 100 is 100*100=10000 comparison, 
Today's average computer requires 1 second to do xx comparisons and 1 second is like an eternity in computer time. 
And although my game will probably have only like 30 agents and the naive implementation will work just fine, are you even programmer if you are not optimising for requirements you'll never need. 

After looking around, I learned about quad trees and it can improve the performance significantly. A box at top right of a screen need not bother about another box in bottom left of the screen. So the idea is to look at only a small area for each box so that we make fewer comparisons. 
I learned enough to implement one on my own but figured that I would rather use a library. I used the one made by the coding train. (In a future Blog I will implement one myself and use it in this project)

I use the qTree to "query" nearby agent and see if they intersect. I change the color of inemtersecting boxes to see if the mechanics works. And it does!!! 

Wow I can see the project finished I thought.

Next is to learn about the random movement and still have it behave like bouncing boxes. At this point I realised my life would be a lot easier if I think about the movement interms of geometric vectors. This is how every game does it. So I took my time to learn a little bit about vectors and movement using vectors. And p5 has buitlin vector support. Fantastic. 

Now I had to migrate my primitive x y coordinates to position vector and velocity vector. It was not too much work. I use a position vector to substitute my x,y coordinates and use a velocity vector for movement. Every frame add to the position vector, the velocity vector and it simulates motion. It looks like this 


For jitter motion, we can add a vector with random coordinates and add to the position. We will look into more details later.

Every agent needs to find an "opposing" vector which is closest to itself and move towards it. I'm most embarrassed about this part of my code. I tried several ways but this was the only way it worked.

Some tries : 

Explain the jitter experience
Having ununiform distribution makes it move at a particular direction every time 

All the tries 

Finally everything is put together and here's the result 



Credits and other resources 

Please leave your comments and feedback 




Needs to be more defined 
Needs to be easier to read 
Needs more humour 
Needs a consistent language and tone 
Needs to be serious where required. 
Embedding tweet into the blog 
Enabling comments 
Embedding p5 sketches
Can be more concise but reads fluidly ? 
Informal but informative 






