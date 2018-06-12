---
layout: single
title:  'How to upgrade Git on Mac (OSX)'
date:   2018-6-11 11:32:29 -0400
categories: tools
tags: git, homebrew, brew, mac, macOS
header:
  image: /assets/images/how-to-upgrade-git-mac.jpg
---

Recently a [vulnerability in Git](https://threatpost.com/bug-in-git-opens-developer-systems-up-to-attack/132395/) was discovered that could lead to arbitrary code execution when a developer utilizes a malicious repository. The good news is that this issue has been patched and the fix is available in version [2.17.1](https://marc.info/?l=git&m=152761328506724&w=2).  

Now let's upgrade!

## Overview
In this guide we are going to walk through how to upgrade Git via [Homebrew](https://brew.sh).  First we will install Homebrew and then install Git. Given that you may have Git already installed (e.g. via XCode), this guide will also walk you through how to change your path to use the official (non-Apple) distribution.

### A few details before we get started:
If you are unfamiliar with Homebrew, it is a package manager for Mac that allows you to easily install and utilize a myriad a programs (i.e. formulae).

- For this guide, I am assuming you are running MacOS 10.11 or higher
- Additionally, check out the full Homebrew system requirements [here](https://docs.brew.sh/Installation) before diving in

## Step by Step Guide

### Install Homebrew
_if Homebrew is already installed, you can skip to the Git section_
{% highlight shell %}
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

For installation details, including system requirements check out the documentation [here](https://docs.brew.sh/Installation)

### Update Homebrew to ensure you are on the latest version
{% highlight shell %}
brew update
{% endhighlight %}

### Run brew doctor to ensure everything is good to go
{% highlight shell %}
brew doctor
{% endhighlight %}

If all is well, the output should say `Your system is ready to brew.`

Now let's get to Git.

### Check your current version of git
{% highlight shell %}
git --version
{% endhighlight %}

If the version of git says something like `git version 2.15.1 (Apple Git-101)` then you are running the Apple version of Git, not the official distribution.

No worries, Homebrew has got us covered.

### Install git via Homebrew
{% highlight shell %}
brew install git
{% endhighlight %}

### Change your local path to the Homebrew version
{% highlight shell %}
export PATH=/usr/local/bin:$PATH
{% endhighlight %}

### Check the git version
{% highlight shell %}
git --version
{% endhighlight %}
You should now see the current version of git, such as `git version 2.17.1`.

### To upgrade in the future, simply run
{% highlight shell %}
brew upgrade git
{% endhighlight %}

## Conclusion
We are all set! Homebrew is installed, Git is installed, and we have changed our path to point to the current version.  For further details on Homebrew and some additional resources, check out the links below.

## Additional Resources
- [Homebrew](https://brew.sh)
- [Homebrew Documentation](https://docs.brew.sh)
- [How to use the Homebrew installed Git](https://apple.stackexchange.com/questions/93002/how-to-use-the-homebrew-installed-git-on-mac)
- Updating paths for Git on [StackOverflow](https://stackoverflow.com/questions/1835837/git-command-not-found-on-os-x-10-5)
- [Step-by-Step on How to Update Git on Mac](https://www.michaelcrump.net/step-by-step-how-to-update-git/)
