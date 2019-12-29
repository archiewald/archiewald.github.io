---
title: Web development setup on Ubuntu
key: react-ts-1
tags: tools
image: /assets/images/4-cover.jpg
cover: /assets/images/4-cover.jpg
description: Basic web development setup on Ubuntu
---

A shortlist on how I create a basic web development setup on Ubuntu system. Not really a blog post, something to warm up after I abounded blogging for some time, definitely needed such thing, maybe you find it useful too.

<!--more-->

<figure>
  <img src="{{ "/assets/images/4-cover.jpg" | absolute_url }}" alt="hacker">
  <figcaption>
    by <a href="https://unsplash.com/@hidd3n">Kevin Horvat</a> 
  </figcaption>
</figure>

## Shell

[Zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)
```sh
sudo apt install zsh
chsh -s $(which zsh)
```

[Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh#basic-installation)
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
if 

```
The command could not be located because '/snap/bin' is not included in the PATH environment variable
```
[Path error solution](https://stackoverflow.com/questions/57121916/the-command-could-not-be-located-because-snap-bin-is-not-included-in-the-path) 

## Code editor

[Snap](https://snapcraft.io/)
```sh
sudo apt install snapd
```

[Visual Studio Code](https://snapcraft.io/vscode)
```sh
sudo snap install code --classic
```
set up as default code editor

```sh
xdg-mime default code.desktop text/plain
```

## git/github

[xclip](https://github.com/astrand/xclip)
```sh
sudo apt install xclip
```
Follow:
- [authenticate to github with zsh](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
- [manage multiple github/gitlab accounts](https://medium.com/the-andela-way/a-practical-guide-to-managing-multiple-github-accounts-8e7970c8fd46) - for example home with work one


## yadm

```sh
sudo apt install yadm
yadm clone https://github.com/archiewald/dev-configs.git
```
Set powerline font in editor/terminal

## jekyll

follow [this](https://jekyllrb.com/docs/installation/ubuntu/)

## node

follow [this](https://github.com/nodesource/distributions#debinstall)
