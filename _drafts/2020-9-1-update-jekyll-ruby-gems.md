---
layout: single
title:  'Update Jekyll and Ruby'
date:   2020-8-31 5:00:00 -0400
categories: leadership
tags:
header:
  image:
---
So Yeah, I always forget how to update My gems when I need to. I am not familiar with Ruby and only use it to power my blog.  Two challenges happen: 1) sometimes things get out of date and I just want to update to stay current and 2) I get security alerts from GitHub and need to (have to) update to stay secure. The challenge? I _always_ forget how to do it. So...to stop that I am going to fix an GitHub security issue now and document my steps on how I did it.

# Jekyll

# Homebrew
How do I make sure homebrew is up to date?
`brew outdated`

# Ruby
First, how do I check my version of ruby?
`ruby -v`

Using `rvm` install the latest version of ruby
`rvm install ruby --latest`

to install a specific version you can do
`rvm install ruby-2.5.0`

After updating Ruby you may need to update the bundler
`bundle update --bundler`

or to install
`gem install bundler`

install a specific version
`gem install bundler:1.18.2`

gems are for ruby. bundler installs ruby gems. Gems are packages.

Once I updated ruby, jekll did not not work (it was actually not found), to address this, I ran
`bundle update --bundler`

to update all gems (this is what did the fix for me)
`bundle update`

to update a specific gem
`gem update <GEMNAME>`
for example

`gem update <GEMNAME>`

## Resources
- https://jekyllrb.com/docs/installation/macos/
- https://docs.brew.sh/FAQ
- https://bundler.io/v2.1/man/bundle-update.1.html
- https://medium.com/@IanRahman/how-to-upgrade-ruby-on-a-mac-a592c6085c63
