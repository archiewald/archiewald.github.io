---
title: How to fix an npm package
tags: npm typescript
---

It might happen that an npm package you want to use has some bugs. Should you just wait for maintainers to fix them? Sure not 😉. You can eliminate the bug and host package by yourself. Then create a pull request and possibly become an open-source contributor&nbsp;💪.

<!--more-->

<figure>
  <img src="{{ "/assets/images/1-collaboration.jpg" | absolute_url }}" alt="collaboration">
  <figcaption>
    by <a href="https://unsplash.com/photos/a2VqhP3d4Vg?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">rawpixel</a> 
  </figcaption>
</figure>

## Bugs happens 🐛

Recently I used a [react-ga](https://www.npmjs.com/package/react-ga) npm package to connect React based Single Page App to Google Analytics services.

To start I followed an usual procedure, including `react-ga` in `package.json` file. `npm install` went well, then on `npm start`:

```shell
Failed to compile.

/Users/arturkozubek/projects/orbicobeauty-web/node_modules/react-ga/types/index.d.ts
(87,20): A rest parameter must be of an array type.
```

🙀 This is unusual... Clearly there is a TypeScript related bug in this package... Having a look on the mentioned `index.d.ts` file, line 87:

```typescript
export function ga(...args: any): void;
```

Well, I guess I just follow the message of TypeScript compiler and make it:

```typescript
export function ga(...args: any[]): void;
```

So I saved the changes locally and tested. It worked! But you can't just rely on modifying a node module source files... You probably ignore `node_modules` files in your repo, which is a good common practice. Any time you (or your colleague) reinstall the package it will be downloaded again from original source.

## Fork and use 🍴

Usually (if not always, not sure) package source code is served on github. What's more, you can point a github repository in `package.json` to download a package from there. Can you see where it goes 😉?

1. I forked the package,
2. cloned to my machine so I can edit the source code `git clone https://github.com/archiewald/react-ga.git`,
3. fixed the bug as before,
4. just pushed the commit to master.

In `package.json`, instead of version number, I pointed to the repo I just forked and created, with commit hash to make it explicit what code I refer to:

```json
{
  ...

  "react-ga": "git+https://github.com/archiewald/react-ga.git#e9d592e940260017f23815bcee9703a2a4866705",

  ...
}
```

After re-`npm install` I could enjoy implementing this great package!

## Contribute 💪

Don't be afraid to share your fix with the community! Raise [an issue](https://github.com/react-ga/react-ga/issues/342) and create [a pull request](https://github.com/react-ga/react-ga/pull/343) with your changes. Once you implemented them in your forked repo, it is so easy!

<figure>
    <img src="{{ "/assets/images/1-pull-request.png" | absolute_url }}" alt="pull request">
    <figcaption>
      Fix => contribute
    </figcaption>
</figure>