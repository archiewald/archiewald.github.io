---
title: How do I share my bookmarks on the web
key: awesome-bookmarks
tags: tools node javascript git
image: /assets/images/6-bookmarks.png
cover: /assets/images/6-bookmarks.png
---

Whenever I read something valuable around software engineering I save it in categorized browser bookmarks. You can find them in the Awesome section on this website as well. In this article I described how they are kept in sync.

Find the repo [here](https://github.com/archiewald/awesome-links)

<!--more-->

<figure>
  <img src="{{ "/assets/images/6-bookmarks.png" | absolute_url }}" alt="bookmarks picture">
  <figcaption>
    by <a href="https://unsplash.com/@quasichiara">Chiara F</a> 
  </figcaption>
</figure>

I thought it would be worth sharing them with the world. As for myself, I would love to see what particular materials my colleagues find interesting.

So there are bookmarks in my browser and the platform I use to share my thoughts is this very blog. How about creating a page with a list of awesome links, kept in sync with my bookmarks so I don't need to upload it manually each time I add a new awesome article.

This blog is using [jekyll](https://jekyllrb.com/) platform to create and deploy content on GitHub in a famous [Jamstack](https://jamstack.org/) manner. The process of how I create a blog post is:

- create a markdown file with the article content in a [blog repository](https://github.com/archiewald/archiewald.github.io)
- as far as the article is `git push`ed, GitHub handles the build process, deploy and make it available to the world. The process is so simple because of [GitHub Pages & Jekyll integration](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll)

Coming back to the bookmarks, the first step was to check how I can approach them in a machine-friendly manner to automate the process. The answer I found was [chrome.bookmarks api](https://developer.chrome.com/extensions/bookmarks) available for Google Chrome extensions.

With the above knowledge I came out with the process on how to go from awesome bookmarks to the awesome links page on my blog:

1. Create a chrome extension able to get my bookmarks
1. Send serialized bookmarks over HTTP to a simple node app
1. On the node app:

- Clone the blog repository
- Parse bookmarks and create awesome-links.md page which will be compiled to a HTML page in build process later
- Commit changes and push to the repo

1. Wait until the page is deployed and available on [kozubek.dev/awesome-links](https://www.kozubek.dev/awesome-links.html)

## chrome extension

Bookmarks are available as a tree, getting them and sending to the node app was pretty straightforward:

```js
function sendAwesomeBookmarks() {
  chrome.bookmarks.getTree(async (bookmarks) => {
    const awesomeBookmarks = bookmarks[0].children
      .find(({ id }) => id === "1")
      .children.find(({ children, title }) => children && title === "awesome")
      .children.map(({ title, children }) => ({
        title,
        children: children.map(({ title, url, id }) => ({ id, title, url })),
      }));

    await fetch(process.env.API_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        bookmarks: awesomeBookmarks,
        secret: process.env.SECRET, // more on that later ;p
      }),
    });
  });
}
```

## How to handle git operations in a node app

I tried some git specific node libraries like [nodegit](https://github.com/nodegit/nodegit) and it was a hard experience. I felt like I used an overcomplicated tool for basic git operations, whereas you can simply run a shell command from your node script with a built-in `child_process` library.

```js
const util = require("util");
const exec = util.promisify(require("child_process").exec);

async function main() {
  await exec('git clone "https://github.com/archiewald/archiewald.github.io"');
  const { stdout } = await exec("git status", {
    cwd: "./archiewald.github.io", // required if you want to run a command in a different folder
  });
  console.log(stdout); // On branch master Your branch is up to date with 'origin/master'...
}

main();
```

Few things happen here. Since most of the node api was built when promises were not available yet, typically it uses callbacks to handle asynchronous operations which results in hardly maintainable code because of [callback hell](http://callbackhell.com/). That's why we wrap it with, builtin as well, `util.promisify()`. It's doing a great job transforming a callback style `(err, value) => ...` function into a version that returns a promise.

Interestingly, there is a `util.callbackify()` function available as well, if you need one :)

On the other hand, the file system library has a promises API already available via `require("fs").promises`.

## Making it secure enough

A disclaimer: I consider below solution good enough for my personal scripting project but it shouldn't be used in production for customer-oriented web apps - keeping API Access Tokens on the client side hardcoded wouldn't be a good idea!

I needed some pain-free GitHub integration to commit updated bookmarks to the blog repo. As I learned, perhaps the easiest to do it is passing the credentials when cloning the repository:

```sh
git clone "https://<GIT_USERNAME>:<GIT_PERSONAL_ACCESS_TOKEN>@github.com/archiewald/archiewald.github.io
```

But I wouldn't dare to pass my personal, real GitHub account credentials there. I came out with a hacky solution - just creating a new GitHub user with the one and only responsibility - to commit and push awesome bookmarks updates. Then the account was added as a collaborator to this particular repo.

<!-- picture -->

Another problem is how to keep my credentials out of the repository. You can create an `.env` file to be consumed by webpack so the api url and secret are injected in the build process:

```js
// in .env

API_URL="awesome-links.example.com";

// in webpack.config.js:

const webpack = require("webpack");
const dotenv = require("dotenv");

module.exports = {
  plugins: [
    new webpack.DefinePlugin({
      "process.env": JSON.stringify(dotenv.config().parsed),
    }),
  ],
};

// in script.js:

await fetch(process.env.API_URL);

// in build/script.js:

await fetch({ API_URL: "awesome-links.example.com" }.API_URL);
```
