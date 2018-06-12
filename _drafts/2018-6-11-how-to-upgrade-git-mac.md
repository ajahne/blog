---
layout: single
title:  'How to upgrade Git on your Mac (OSX)'
date:   2018-6-11 11:32:29 -0400
categories: javascript
tags: nodejs, homebrew, brew, mac, macOS
header:
  image: /assets/images/evolution-of-my-1-on-1s.jpg
---

Recently a [vulnerability in Git](https://threatpost.com/bug-in-git-opens-developer-systems-up-to-attack/132395/) was discovered that could lead to arbitrary code execution when a developer utilizes a malicious repository. The good news is that this issue has been patched and the fix is available in version [2.17.1](https://marc.info/?l=git&m=152761328506724&w=2).  

Now let's upgrade!

## Overview
If you are using a Mac (as I am) then you may typically upgrade Git via XCode (e.g. system update).  However, what if you want (need) to upgrade (like now).  Wouldn't it be great to upgrade via a simple command in the terminal?

In this guide we are going to walk through how to upgrade Git via Homebrew.  First we will install Homebrew (if not installed already) and then install Git. Given that you may have Git already installed (e.g. with XCode), you will have to change your path.  We got you covered

Step by step guide coming up!

## Before we get started:
- I am assuming you are running MacOS 10.11 or higher
- Check out the full system requirements [here](https://docs.brew.sh/Installation)

## Steps

### install homebrew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
For installation details, including system requirements check out the documentation [here](https://docs.brew.sh/Installation)


### update homebrew to ensure you are on the latest version)
```
brew update
```

### run brew doctor to ensure everything is good to go
```
brew doctor
```

Output should be say `brewed...`

### check your current version of git
```
git -v
```

If the version if git says something like
`git version 2.15.1 (Apple Git-101)`
then you are running the Apple version of Git, not the official version.

No worries, let's switch it up

### install git via homebrew
```
brew install git
```

### change your local path to the homebrew version

- what is home brew? Package manager for mac
- install node
- check installation, you're done!

Helpful links
- [Homebrew](https://brew.sh)
- [Homebrew Documentation](https://docs.brew.sh)
