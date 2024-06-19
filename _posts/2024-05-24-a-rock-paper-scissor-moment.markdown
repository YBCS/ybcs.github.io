---
layout: post
comments: true
title:  "A Rock Paper Scissor Moment!"
excerpt: "Analyzing a rock paper scissor simulation"
date:   2024-05-24 00:35:45 +0530
categories: tech blog
---
### A `Rock`, a `Paper`, and a `Scissor` Enter a room....

<img src="/assets/ScreenshotRPS.png" width="30%" />

####  Play it <a href="https://ybcs.github.io/RPS_Play/" target="_blank">HERE</a>


We all know the classic rules:
  > `Rock` > `Scissors`  
  > `Paper` > `Rock`  
  > `Scissors` > `Paper`  

But what if these objects had more in common? Let’s imagine they all start as `"Agents"` with shared properties like movement behavior, position, and velocity.

### Agents and Their Environment

Each agent needs to be aware of other agents. Imagine an environment full of these agents. If each agent tries to compute the location of every other agent, it becomes a very complex and slow process because each agent has to consider all others. This is called a quadratic operation. 

Each agent's field of view (awareness range) covers the whole environment. Which means each agent can see all other agents. Not very efficient.

### Optimizing with Quadtrees

To make this process faster, the environment can use optimization technique like quadtree (more information below). This heps reduce the number of computations. Instead of seeing the entire environment, an agent only looks at a smaller area around it. For example, agents in opposite sides of the environment does not need to know about the other.

### Specialized Agents: Rock, Paper, Scissor

Now, let's specialized the agents into roles: rock, paper or scissors. Let's Call them RoleAgent (feel free to suggest a better name in the comments!).  

Think of each RoleAgent as having predator-prey relationship based on the classic rules:
  > `Rock (predator)` > `Scissors (prey)`  
  > `Paper (predator)` > `Rock (prey)`  
  > `Scissors (predator)` > `Paper (prey)`  

A predator RoleAgent will look for its closest prey withing its range(field of view), move towards it, and "transform" it into another predator. It's a bit like Zombie behaviour!. 

### What is a QuadTree?
> A quadtree is a tree data structure in which each internal node has exactly four children. Quadtrees are the two-dimensional analog of octrees and are most often used to partition a two-dimensional space by recursively subdividing it into four quadrants or regions.  --wikipedia

### Got Questions?
If you have any questions, feel free to leave a comment! I'm also active on [X (Twiter)](https://x.com/Budhachandra_) and email.

### References
- [Souce Code of Project](https://github.com/YBCS/RPS_Play)
- [Tweet which inspired this side project](https://x.com/juanbuis/status/1600155605112496129)
- [QuadTree explanation by The Coding Train](https://youtu.be/OJxEcs0w_kE)