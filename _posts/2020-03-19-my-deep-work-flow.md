---
title: Deep work app I am about to create
key: deep-work-flow
tags: tools
image: /assets/images/5-woodwork.jpg
cover: /assets/images/5-woodwork.jpg
description: yet another pomodoro app we need
---

I am creating a tool to help with focused yet healthy work with a computer. Doing it for myself because I didn't find an app which meets my expectation in 100%. I don't plan to make a fortune out of it, rather develop a simple open-source, free to use app.

<!--more-->

TLDR: pomodoro 🍅 timer + todo-list + healthy habits reminder + reports to track your progress. Does it click for you? Please read further and let me know what do you think in the comments.

<figure>
  <img src="{{ "/assets/images/5-woodwork.jpg" | absolute_url }}" alt="woodworker">
  <figcaption>
    by <a href="https://unsplash.com/@bobrodriguez">Filipe de Rodrigues</a> 
  </figcaption>
</figure>

## Struggling to stay focused

Looking back in the past I reckon myself as a kid who was hard to distract from a cognitive task. If there was a piece of work to be made and I enjoyed it - like preparation for a math competition, physics test - it was relatively easy for me to stay focused for a few hours. That stuff was quite comparable to my current day to day work. Yet I feel now it is much harder for me to keep myself undistracted. Had anything changed since that time?

Certainly it did. To start with, I work on a computer. All day long. I don't think this will ever change - maybe the form of what a personal computer itself is, but I am pretty sure I will be around creating/handling digital products - like many of us.

And as much as I love it and feel this is a right environment for me, being able to stay focused on an assigned task becomes much more challenging. Digital services I daily use are craving for my attention all the time. With the content, with the way they look, with the User Experience they offer. There are top paid engineers and marketers who have a clear goal - make me stay on their portals as long as it is possible and bring me back when I leave.

## Deep work as a valuable skill

Another interesting perspective I got from a book [Deep Work](https://www.goodreads.com/book/show/25744928-deep-work) by Cal Newport. What he says makes much sense with my experience - staying focused on a task gets harder so learning it gives you a competitive advantage.

> One of the most valuable skills in our economy is becoming increasingly rare. If you master this skill, you'll achieve extraordinary results.<br><br>
> Deep work is the ability to focus without distraction on a cognitively demanding task. It's a skill that allows you to quickly master complicated information and produce better results in less time. Deep work will make you better at what you do and provide the sense of true fulfillment that comes from craftsmanship. In short, deep work is like a super power in our increasingly competitive twenty-first century economy. And yet, most people have lost the ability to go deep-spending their days instead in a frantic blur of e-mail and social media, not even realizing there's a better way.

## 🍅⌚

I arranged a toolset to fight with digital interruptions. Pomodoro technique is I believe the most important one. How it works? After [the author](https://francescocirillo.com/pages/pomodoro-technique)

> 1. Choose a task you'd like to get done
> 1. Set the Pomodoro for 25 minutes
> 1. Work on the task until the Pomodoro rings
> 1. When the Pomodoro rings, put a checkmark on a paper
> 1. Take a short break
> 1. Every 4 pomodoros, take a longer break

It works very well for me when I'm programming or writing. Every time I switched OS I find some app to serve me :

- on macOS I used [beFocused](https://xwavesoft.com/be-focused-pro-for-iphone-ipad-mac-os-x.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier)
- on Linux I used [Gnome Pomodoro](https://gnomepomodoro.org/)
- on Windows I am using [Pomotodo](https://pomotodo.com/) - actually the best among these

Clearly I can call myself a pomodoro app heavy user :)

## Work ergonomics

Who made me think about it was a lecturer at Berkeley University of Computer Science course I used to listen.

We rarely have an opportunity to listen the elder people talking about using a computer or programming. So I believe if one has some piece of advice for you it worths listen:

<div class="videoWrapper">
  <iframe src="https://www.youtube.com/embed/8aFp84teahw?start=81" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Among the few rules he mentions, the most important one - take a break every ~ half an hour. Plays very well with Pomodoro technique, right?

These breaks we can use even further for our health. Sure there is an app for this purpose, let me introduce you [Safe Eyes](https://slgobinath.github.io/SafeEyes/).

<figure>
  <img src="{{ "/assets/images/5-safe-eyes.png" | absolute_url }}" alt="safe eyes">
  <figcaption>
    Safe Eyes break screen  
  </figcaption>
</figure>

It does a great job of presenting you exercise each break, preventing you from repetitive strain injuries (RSI). But, in my case, it needs to be in sync with pomodoro app as well so using it day to day was a pain in the ass.

## The perfect app

What would make a great tool to enhance a deep and healthy workflow with a computer?

- a tomato timer with editable work/break/long break time
- present healthy short exercises to do each break
- ability to put the pomodoros I have done in some context (simple todo-list and/or tagging system like #work #blog #studies etc)
- statistics of how much deep work time I was able to perform each day/week
- get reports presenting above with some nice looking charts (in weekly emails?)
- multiplatform desktop app - would like it to run on Windows/macOS/Linux since I tend to switch between them a lot

The closest I found is [Pomotodo](https://pomotodo.com/), but it doesn't have the healthy tips and is not so UX friendly, at least the Windows version.

## About the tech

So, I am about to make such. I am excited to use [Progressive Web App](https://youtu.be/2KhRmFHLuhE) approach to create a multiplatform app, it seems like PWA support on desktop should bring me there ❤.

It is far from being finished but is already useful enough for me to use it - basic pomodoro timer with desktop notification.

Here it is, [Yet Another Pomodoro App (CLICK ME)](https://www.kozubek.dev/yapa-frontend/). It is super simple and ugly. As long as you open it in Google Chrome on any system, you should be able to install it as a stand-alone, offline first app. It is a website but you don't need an internet connection to use it after you enter it! This is probably the future of how apps, both desktop and mobile, will be distributed.

<figure>
  <img src="{{ "/assets/images/5-yapa.png" | absolute_url }}" alt="yet another pomodoro app">
  <figcaption>
    the ugliest pomodoro app - installable and offline first
  </figcaption>
</figure>

[Code repository](https://github.com/archiewald/yapa-frontend)

## What next

I am about to add next features to [Yet Another Pomodoro App](https://www.kozubek.dev/yapa-frontend/) (and think about some proper name, though YAPA acronym sounds tempting). And sure, polish it to look much better ;) Would love to get some feedback about the idea. Do you find such problems in your workflow? Do you use any tools in this area that I might check for reference? Would you use YAPA when it's finished? Let me know guys!
