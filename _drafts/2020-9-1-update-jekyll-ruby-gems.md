---
layout: single
title:  'Notes on Updating Jekyll and Ruby on macOS'
date:   2020-8-31 5:00:00 -0400
categories: tools
tags: jekyll, ruby, gems, bundle, homebrew, macOS
header:
  image:
---
So yeah, I always forget how to update my gems when I need to. I am not familiar with Ruby and only use it to power my blog.  Two issues often occur:
1. Gems get out of date and I just want to update to stay current and/or
2. I get security alerts from GitHub and need to (have to) update to stay secure

The challenge? I _never_ remember how to do it. So...to stop that I recently took a few notes 📝 while I fixed a GitHub security issue related to my blog. Below are some command line tools that I ran while debugging and fixing. I plan to update this post over time as needed.

Similar to my write up on [updating Git for macOS]({{ site.baseurl }}{% post_url 2018-6-11-how-to-upgrade-git-mac %}), this is meant to be notes and helpful information, not the gospel. Use discretion if/when using 😀.


**TL;DR**
- `bundle install` installs what is currently in the `Gemlock.file`
  - If any errors happen when starting Jekyll, run the above command above **first**
- Update specific gems with `bundler` (e.g. `bundle update <GEMNAME>`)
- If you need to update Ruby run `rvm ruby --latest`
- Make sure dependencies align with the [GitHub pages dependency list](https://pages.github.com/versions/)

# Jekyll

Check Jekyll version
```sh
jekyll -v
```

[Update](https://jekyllrb.com/docs/upgrading/) Jekyll
```sh
bundle update jekyll
```

Run Jekyll
```sh
jekyll serve
```

Run Jekyll with drafts
```sh
jekyll serve --drafts
```

_More command options are listed [here](https://jekyllrb.com/docs/configuration/options/#build-command-options)_

---

# Ruby
Check Ruby version
```sh
ruby -v
```

Install the latest version of Ruby (using RVM)
```sh
rvm install ruby --latest
```

Install a specific version of Ruby (using RVM)
```sh
rvm install ruby-2.5.0
```

## Ruby [Bundler](https://bundler.io)
Install the bundler
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

To install gems that have been previously installed based on the `Gemfile.lock`, run
```sh
bundle install
```

![jekyll serve before bundle install]({{site.baseurl}}/assets/images/update-jekyll-ruby-error.png){:height="100%" width="100%"}

_Note: Previously when Jekyll did not not work (see image above), I ran the `bundle install` to address this_

To update all gems _(Note: probably better to run `bundle install` as that uses the `Gemfile.lock`)_
```sh
bundle update --all
```

To update a specific gem
```sh
bundle update nokogiri
```

---
# Other tools, Notes, and Miscellaneous:

## Homebrew
First update the formulae and Homebrew
```sh
brew update
```

Find out what is out of date
```sh
brew outdated
```

Upgrade a specific formula
```sh
brew upgrade git
```

## Ruby Gems
Gems are for Ruby. Gems are packages. Bundler installs ruby gems.

To [update](https://guides.rubygems.org/command-reference/#gem-update) a specific gem. Note: [seems better to use bundler for application specific updates](https://stackoverflow.com/questions/4604064/rubygems-bundler-and-rvm-confusion)
```sh
gem update <GEMNAME>
```

## Additional Resources
- [Install Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)
- [Bundler](https://bundler.io/v2.1/man/bundle-update.1.html)
- [Ruby Gems](https://guides.rubygems.org/rubygems-basics/)
- [RVM](https://rvm.io/rvm/upgrading)
- [How to update Ruby on a Mac](https://medium.com/@IanRahman/how-to-upgrade-ruby-on-a-mac-a592c6085c63)
- [Homebrew Cheatsheet](https://devhints.io/homebrew)
- [How to upgrade Git on macOS]({{ site.baseurl }}{% post_url 2018-6-11-how-to-upgrade-git-mac %})
- [Homebrew FAQ](https://docs.brew.sh/FAQ)
