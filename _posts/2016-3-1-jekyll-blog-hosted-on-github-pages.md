---
layout: post
title: Jekyll Blog Hosted on GitHub Pages
---

## Install Jekyll on mac

First install ruby from Homebrew (`brew`):

```bash
brew install ruby
```

Make sure `/usr/local/bin/` is in your `$PATH`.

Then install Jekyll by RubyGems (`gem`)

```bash
gem install jekyll
gem install jekyll-sitemap
gem install github-pages
gem install pygments.rb
```

## Fork a jekyll site on GitHub

As a GitHub user, you’re entitled to one free "user" website (as opposed to a "project" website), which will live at http://yourusername.github.io. This space is ideal for hosting a Jekyll blog!

The best part is that you can simply place your unbuilt Jekyll blog on the master branch of your user repository, and GitHub Pages will build the static website and serve it for you. You don’t have to worry about the build process at all -- it’s all taken care of.
Click the "Settings" button in your new forked repository (in the menu on the right), and change the repository’s name to `yourusername.github.io`, replacing yourusername with your GitHub user name.

Your website will probably go live immediately. You can check by going to http://yourusername.github.io.

## Local modification and Push

Then `cd` to some directory, and clone the repository you just forked.

```bash
git clone https://github.com/yourusername/yourusername.github.io.git
```

Create a new post in the `_posts` folder. Remember to name it in the format `year-month-day-title.md`, and include the front matter at the top of the post.

Commit the post’s Markdown file, and push to your GitHub repository.

That’s it! Just wait for GitHub Pages to rebuild your website.

You can view your site locally

```bash
jekyll serve
```

then browse [http://127.0.0.1:4000](http://127.0.0.1:4000).

### Read More
[1] [Jekyll Project Homepage](https://jekyllrb.com)

[2] [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/), By Barry Clark

[3] [GitHub Pages](https://pages.github.com)
