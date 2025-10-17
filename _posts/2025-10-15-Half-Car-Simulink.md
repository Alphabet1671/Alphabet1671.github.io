---
layout: post
title:  "My Take on Platform Control for FSAE"
date:   2025-10-17 00:00:00 -0500
categories: Technical
tags: VD
---

## Introduction

If you have aero on your car, congrats because your team can pull it off. However, it does create a problem: sometimes they dig into the ground. If you look at it from just a suspension designer's point of view, the problem would be simple: somehow make that car stiff enough in roll and pitch so that it doesn't. But like all other good things that happen in engineering, it always comes with a catch. 

This graph here illustrates the problem of stiffness and contact patch load variation (CPLV) that's obtained from a state-space linear half car model:
[insert image here]

When the wheel load fluctuates, so does the available grip, and when it does that a dozen times a second, the car ends up being able to use no more than the minimum grip at a particular short time period. So, the more it fluctuates, the lower the minimum. This means that CPLV is a pretty good indicator of mechanical grip. In other words, generally, the stiffer the car is, the less mechanical grip it has.

Now we see that we have a trade study at hand. A lower car can generally give good aerodynamic performance due to ground effects, but a lower car will have worse mechanical grip due to it being stiffer from a higher desired roll/pitch gradient.

Now of only there's a way to make the car stiffer in pitch only when it's pitching, and stiffer in roll only when it's rolling...

See, you've just described anti geometry and roll centers, while they do the job just fine, it leaves very little room for adjustment unless you feel like machining 16 new A-arm hardpoint brackets every single time you want to tune your car (which some motorsports actually do). 

So if you can't use kinematics, what else could you possibly do? Well, think about what makes the car scrapes a lot: large bumps, heavy braking, and high speed cornering roll. All of these have something in common: they command a lot of suspension travel. So imagine if your suspension gets stiffer as it travels, that would mean that it would retain good mechanical grip at low speed with less acceleration, and then get high stiffness when the car is close to scraping. 

There are a few ways of achieving this concept: 
- Progressive springs: springs that increase in pitch.
- 2 stage springs: two springs in series, one short and soft, the other long and stiff.
- 3rd springs & ARB: auxiliary roll/pitch stiffness, can be configured to only engage after a certain point.
- Mode decoupled: new hot kid on the block in FSAE Michigan, useful if your car is scraping only in pitch or roll.

The idea of this series of posts is that: given any arbitrary FSAE car, how would one go about picking the optimum architecture? And how would one balance aerodynamic and mechanical grip?

[This paper](https://radar.brookes.ac.uk/radar/file/7fc3dce7-8da4-4362-a5dc-df16a19c1683/1/bennett2012ride.pdf) provides a good method of condensing the vertical dynamics characteristics into a simple grip loss scalar. This means that, with a simple vertical dynamics suspension test rig data, one could obtain how much grip is lost due to body/wheel hop. In terms of aero grip, given a certain body attitude, one could obtain the downforce from CFD, so it can also be condensed into a singular scalar of aero grip at any given moment on the track, and finally reaching an average over a single lap of the track.

## Tool Building

Knowing that it's possible to trade aero/mechanical grip, all we need is a shaker rig for the car. Of course, not every school has one, so we're going to settle with a half car Simulink rig. Here's the [Github link](https://github.com/Alphabet1671/FSAE-VD-Personal-Scripts) to the one that I've built.

The associated Matlab script under the Vertical Dynamics folder drives damper curve sweeps.

### Work in Progress...



