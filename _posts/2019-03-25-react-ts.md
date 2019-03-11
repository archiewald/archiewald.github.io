---
title: Introduction to React with TypeScript
key: react-ts-1
tags: react typescript
image: 
cover: 
description: TypeScript can help you create maintainable and scalable web apps. It is ready to use with React out of the box!
---

Why you should use React with TypeScript? How to start a TypeScript app with Create React App?

<!--more-->

## Why you should use TypeScript in React

### Gives you a great developer experience

I ❤️ TypeScript for giving me an instant feedback if I am wrong with my code. Look for top 10 JavaScript error. I am sure that as a web developer you know them well.

<figure>
  <img src="{{ "/assets/images/3-js-errors.png" | absolute_url }}" alt="top 10 js errors">
  <figcaption>
    top 10 JavaScript errors in 1000 projects by <a href="https://rollbar.com/blog/top-10-javascript-errors/t">Rollbar</a> 
  </figcaption>
</figure>

7 of them are about mixing up your types, not accessing the right variable, object property etc. With TypeScript you will rarely see this errors! Your configured IDE will tell you about them in advance.

Another thing is code maintaining and refactor. Did you ever modified some property in you large app and went through all the classes and properties wondering what you just fucked up and fixing here and there? Here TypeScript + your IDE will be your help as well.

### It fits React very well

If you ever liked Angular for having a TypeScript support you will love React even more. Template engine from a developer point of view is very different - in Angular you have dummy html files, in React there is JSX, turning into TSX with TypeScript. This means you get static type checking in your templates as well!

### Supported out of the box

As our prophet announced

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Create React App 2.1 + TypeScript = 💜 <a href="https://t.co/tpb04toZ95">https://t.co/tpb04toZ95</a> <a href="https://t.co/zBTVb0qa3U">pic.twitter.com/zBTVb0qa3U</a></p>&mdash; Dan Abramov (@dan_abramov) <a href="https://twitter.com/dan_abramov/status/1057118684479537152?ref_src=twsrc%5Etfw">October 30, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


### Got super trendy last times

<figure>
  <img src="{{ "/assets/images/3-state-of-js.png" | absolute_url }}" alt="js flavors">
  <figcaption>
    State of JS 2019 - <a href="https://2018.stateofjs.com/javascript-flavors/overview/)">JavaScript flavors</a> 
  </figcaption>
</figure>

This post from the react guy

Getting traction of flow https://github.com/facebook/jest/pull/7554#issuecomment-454358729

Interesting view from the inside.


## How to start

### The right IDE

For your best experience you should use VS Code. It is Microsoft open-source IDE and TypeScript is from Microsoft as well. You have the best integration here and I know people moved from WebStorm to VS Code because they start using TypeScript.

> TypeScript is all about developer experience, what is going on in your IDE. How fast and well will you be informed about errors you are about to make 🙂

### Create React App

Let's start with create-react-app package you might already know. It is recommended by CRA creators to use [npx](https://www.npmjs.com/package/npx) to make sure you start with the latest version. We will make use of a fresh new `--typescript` flag.

```terminal
npx create-react-app react-ts --typescript
cd react-ts
```

