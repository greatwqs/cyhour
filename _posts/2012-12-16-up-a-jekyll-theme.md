---
layout: post
title: "UP: A Jekyll theme"
---

After a while using [Jekyll Bootstrap][jekyll_bootstrap], I just realized that it was
so much bloated. Then, few days ago, I forked the old [Zach Holman's blog][zach], and
started to tweak my own theme based on theirs (that now is [opensource][left]). At first,
I like it, but after a while, I just start thinking that it had a "old style" design.

So, I decided to work in my own layout, and then, [**up**][up] was born.

## [Up][up]

[Up][up] is a clean and beautiful [Bootstrap](http://getbootstrap.com) based layout
for [Jekyll](https://github.com/mojombo/jekyll).

It's designed to be an easy layout to modify for your own blog. It was based on
[zachholman's][zach] blog themes: the "old" one, now opensourced as [left][left]
and in his actual theme, that's not opensource (I believe), but I steal some ideas
anyway. I also took something from
[jekyll-bootstrap](https://github.com/plusjade/jekyll-bootstrap), and, of course,
I'm using [bootstrap](https://github.com/twitter/bootstrap) as a base for all the thing.

![Up](http://i.imgur.com/4bKG5.png)

It's fully-responsive (open it in your phone and/or tablet and you will see), with
no JS at all (except twitter button, but you can remove it, of course), with a
custom bootstrap build, compiled and minified with custom CSS in a very small CSS
file (that's why it's really fast). Oh, I almost forgot: it also have an
[atom feed](/atom.xml).

I also steal-and-tweak a Rakefile to made you able to easily create new posts and start
server in preview mode.

## Installation

Up installation is not that hard. Just do this:

- Install Jekyll: `gem install jekyll`
- Fork [this repository][up]
- Rename it to `YOUR-USER.github.com`
- Clone it: `git clone https://github.com/YOUR-USER/YOUR-USER.github.com`
- Run the jekyll server in the blog folder: `rake preview`.

You should have a server up and running locally at `http://localhost:4000`.

## Customization

Next you'll want to change a few things. The list of files you may want to
change is the following:

- [_config.yml](https://github.com/caarlos0/up/blob/gh-pages/_config.yml): Put
your config there, almost everything will be up and running.
- [about.html](https://github.com/caarlos0/up/blob/gh-pages/about/index.html):
Well, that's about you, I would change it if I were you... OH WAIT!
- [CNAME](https://github.com/caarlos0/up/blob/gh-pages/CNAME): If you're using
this on GitHub Pages with a custom domain name, you'll want to change this
to be the domain you're going to use. All that should be in here is a
domain name on the first line and nothing else (like: `example.com`).
- [favicon.ico](https://github.com/caarlos0/up/blob/gh-pages/favicon.ico): This
is a smaller version of my gravatar for use as the icon in your browser's
address bar. You should change it to whatever you'd like.
- [apple-touch-icon.jpg](https://github.com/caarlos0/up/blob/gh-pages/apple-touch-icon.jpg):
Again, this is my gravatar, and it shows up in iOS and various other apps
that use this file as an "icon" for your site.

## Create new posts

Well, that's simple. Just type `rake post title="My awesome new post title"`.

BOOM, your all new post markdown file is created under `_posts` folder.

## Deployment

You should deploy with [GitHub Pages](http://pages.github.com)- it's just
easier.

All you should have to do is rename your repository on GitHub to be
`username.github.com`. Since everything is on the `gh-pages` branch, you
should be able to see your new site at `http://username.github.com`.

## Contributing

If you made a awesome kick-ass change, and believe it would be awesome to **up**,
made a pull-request in [up repository][up]!

I'll be proud to accept your contributions.

## Licensing

This is [MIT](https://github.com/caarlos0/up/blob/gh-pages/LICENSE) with no
added caveats, so feel free to use this on your site without linking back to
me or using a disclaimer or anything silly like that.

If you'd like give [me](http://github.com/caarlos0),
[holman](http://github.com/holman)
(from [left](http://github.com/holman/left)),
[plusjade](https://github.com/plusjade)
(from [jekyll-bootstrap](https://github.com/plusjade/jekyll-bootstrap)) or
[fat](https://github.com/fat) and [mdo](https://github.com/mdo) (from
[bootstrap](https://github.com/twitter/bootstrap)) credit somewhere on your
all-new blog or tweet a shout out to us, well hey, sure we'll take it.

[up]: https://github.com/caarlos0/up
[zach]: http://zachholman.com
[left]: http://github.com/holman/left
[jekyll_bootstrap]: http://jekyllbootstrap.com/
