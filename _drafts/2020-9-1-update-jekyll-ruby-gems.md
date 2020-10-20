---
layout: single
title:  'Update Jekyll and Ruby'
date:   2020-8-31 5:00:00 -0400
categories: tools
tags:
header:
  image:
---
So yeah, I always forget how to update my gems when I need to. I am not familiar with Ruby and only use it to power my blog.  Two issues often occur:
1. Gems get out of date and I just want to update to stay current and/or
2. I get security alerts from GitHub and need to (have to) update to stay secure

The challenge? I _never_ remember how to do it. So...to stop that I recently took a few notes 📝 while I fixed a GitHub security issue related to my blog. Below are some command line tools that I ran while debugging and fixing. I plan to update this post over time.

This is meant to be notes and helpful information, not the gospel. Use discretion when using 😀.


**TL;DR**
- `bundle install` installs what is currently in the `Gemlock.file`
  - If any errors happen when starting Jekyll, run the above command above **first**
- Update specific gems with `bundler` (e.g. `bundle update <GEMNAME>`)
- If you need to update dependencies first, e.g. Ruby then run (`rvm ruby --latest`)
- Make sure dependencies align with the [GitHub pages dependency list](https://pages.github.com/versions/)

# Jekyll

Running Jekyll
```sh
jekyll serve
```

Running Jekyll with drafts
```sh
jekyll serve --drafts
```

Check Jekyll version
```sh
jekyll -v
```

[Update](https://jekyllrb.com/docs/upgrading/) Jekyll
```sh
bundle update jekyll
```
___
---

# Ruby
check my version of ruby?
```sh
ruby -v
```

Install versions of ruby
Use rvm install the latest version of ruby
```sh
rvm install ruby --latest
```

to install a specific version
```sh
rvm install ruby-2.5.0
```

## Ruby [Bundler](https://bundler.io)
To install the bundler
```sh
gem install bundler
```

Install a specific version of the bundler
```sh
gem install bundler:1.18.2
```

After updating Ruby you may need to update the bundler. To update:
```sh
bundle update --bundler
```

_Note to self: Previously when Jekyll did not not work (it was actually not found), I ran the command above to address this_

To update all gems (Note: probably better to `install` as that uses the `Gemfile.lock`)
```sh
bundle update --all
```

To update a specific gem
```sh
bundle update nokogiri
```

To install gems that have been previously installed based on the `Gemfile.lock`, run
```sh
bundle install
```
---
# Other tools, Notes, and Miscellaneous:

Gems are for Ruby. Gems are packages. Bundler installs ruby gems.

## Homebrew
How do I make sure Homebrew is up to date?
```sh
brew outdated
```

## Ruby Gems
To [update](https://guides.rubygems.org/command-reference/#gem-update) a specific gem. Note: [seems better to use bundler for application specific updates](https://stackoverflow.com/questions/4604064/rubygems-bundler-and-rvm-confusion)
```sh
gem update <GEMNAME>
```

## Resources
- https://jekyllrb.com/docs/installation/macos/
- https://docs.brew.sh/FAQ
- [Ruby Gems](https://guides.rubygems.org/rubygems-basics/)
- https://bundler.io/v2.1/man/bundle-update.1.html
- https://medium.com/@IanRahman/how-to-upgrade-ruby-on-a-mac-a592c6085c63
