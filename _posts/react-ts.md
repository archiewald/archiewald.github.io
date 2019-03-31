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

### Tell you about silly errors in advance

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

If you ever liked Angular for having a TypeScript support you will love React even more. Template engine from a developer point of view is very different - in Angular you have dummy html-like files, in React there is JSX, turning into TSX with TypeScript. This means you get static type checking in your templates as well!

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

Let's start with create-react-app package you might already know. It is recommended by CRA creators to use [npx](https://www.npmjs.com/package/npx) instead of installing create-react-app globally, to make sure you start with the latest version.

> Important! Before running below make sure you don't have CRA globally installed anymore! You might encounter issues like [here](https://github.com/facebook/create-react-app/issues/6119)
> ```terminal
> npm uninstall -g create-react-app
> ```

We will make use of a fresh new `--typescript` flag.

```terminal
npx create-react-app react-ts --typescript
cd react-ts
```

and then your TS based app should appear. On this level check if it starts with `npm start`. Let's have a quick look how it differs from regular CRA starter.

> diagram how it differs

### .ts and .tsx files

.ts are regular TypeScript files, they basically replace `.js`. On the other hand, using `.jsx` for files containing React Components with jsx code is not mandatory in js based Create React App. Well, with typescript you need to use `.tsx` 

### What should your ts config have

> TypeScript is like a cool buddy you would like to hang out with and pair program

Lets have a quick look what tsconfig contains. It indicates that the directory is a root of a TypeScript project. It is a starting point for compiler so it contains some configuration options

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve"
  },
  "include": [
    "src"
  ]
}
```

You can look up what particular options are for in [docs](https://www.typescriptlang.org/docs/handbook/compiler-options.html).

An interesting one is `strict` which is provided by default in CRA configuration. Following documentation:

> Enable all strict type checking options. 
> Enabling --strict enables --noImplicitAny, --noImplicitThis, --alwaysStrict, --strictBindCallApply, --strictNullChecks, --strictFunctionTypes and --strictPropertyInitialization.

Strict mode enables you to use all the power of TypeScript and not neglecting all the type checks possibilities. This will have implications in our code but let's talk about it later. You might not turn the `strict` mode if you transfer your JavaScript app to TypeScript but for a start it is definitely recommended.

## Coding an app

Let's clear the app on the beginning, delete `App.css` and leave only dummy skeleton in `App.tsx`

```tsx
import React, { Component } from "react";

class App extends Component {
  render() {
    return (
      <div>
        <h2>Hello React TS!</h2>
      </div>
    );
  }
}

export default App;
```

So far it looks identical to a JS React component. Let's create a first component in `NewTaskForm.tsx`

```tsx
import React, { FunctionComponent } from "react";
import { Task } from "../models/task";

interface Props {
  onChange: (event: React.ChangeEvent<HTMLInputElement>) => void;
  onAdd: (event: React.FormEvent<HTMLFormElement>) => void;
  task: Task;
}

export const NewTaskForm: FunctionComponent<Props> = ({
  onChange,
  onAdd,
  task
}) => (
  <form onSubmit={onAdd}>
    <input onChange={onChange} value={task.name} />
    <button type="submit">Add a task</button>
  </form>
);
```

Let me explain few parts there:

You need to annotate a type to `NewTaskForm` component, which is `FunctionComponent` imported from `react` . Those funny `<>` brackets indicates that this is a [generic](https://www.typescriptlang.org/docs/handbook/generics.html) interface. Thanks to is you can get type checking inside of the component. You are supposed to put your `Props` interface, which describes what properties this component gets from the parent one.

Let's move to the `Props` interface, looking bit cryptic with these callbacks. So `onChange` property expects to get a callback function with one `event` argument. If you ever dealt with forms in React you probably know this one well. We will use data from `event` object in parent component, so we need to annotate the type. It's not that hard as you might think to figure out!

Just move your mouse on 