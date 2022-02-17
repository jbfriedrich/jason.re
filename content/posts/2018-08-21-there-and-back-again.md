---
title: There and back again
date: 2018-08-21T02:36:55
feature_image: https://images.unsplash.com/photo-1511485910951-f7a707918e93?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ&s=d1ceb5a99bfd7225bf1a999f3ff068cd
summary: '"What, you changed your blog? Again?!". That is something I hear very often these days. And they are right, every single one of them.'
tags:
  - blogging
  - tech
  - wordpress
  - en
---

For a while it seemed that I was changing blogging software and blog themes more often than my underwear. But that is all over now, for sure. Maybe… I think…

What happened? Well, I was unhappy with my current blogging software, [Ghost](https://ghost.org), and I was looking for an alternative. I was looking for something easy to use, but it should look good. It should be simple, but have enough "bells and whistles" to be convenient. So I started to try a lot of things...

## Back to the roots

My first idea was to use a Static site generators (SSG). They produce static HTML, which can be cached easily, and hosted for cheap on various sites like [Heroku](https://www.heroku.com), [Netlify](https://www.netlify.com/) or even on [GitHub](https://pages.github.com/) itself. I am very happy with my GitHub Developer account, so why not host my blog there?

I tried two of the more widely used SSG, [Jekyll](https://jekyllrb.com/) and [Hugo](https://gohugo.io/). Both had their advantages and disadvantages. Jekyll clearly was very flexible, very stable, but has a lot of [Ruby](https://www.ruby-lang.org/en/) depdencies. Hugo uses [go](https://golang.org/) which is rather "young", compared to Ruby and other languages. It has the advantage of not having many dependencies. All you need is the binary, and of you "go".

Jekyll and Hugo themes are [widely](https://themes.gohugo.io/) [available](http://jekyllthemes.org/) [online](https://jekyllthemes.io/), if you do not want to create your own. But that is also one of my issues with both SSG. They have a lot of themes, but none of them looked as professional as I wanted to, or as I was used to from the WordPress theme eco system. Some of them use weird hacks, others cannot be used on GitHub, for example, as they only support [certain gems](https://help.github.com/articles/adding-jekyll-plugins-to-a-github-pages-site/).

Once I knew what [Jekyll theme](https://github.com/jekyller/jasper2) I wanted, I started to migrate the blog posts and static pages and moved the images and files from S3 into local directories. Of course, the chosen theme made extensive use of unsupported gems, so it was not enough to upload the source directory to GitHub. I had to build the site manually and commit it to the `gh-pages` branch. It looked nice, but it did not feel quite right.

My experiences with Hugo were similar, almost the same. Go is not supported by Github Pages, which meant that letting Github do the job of generating my site was not an option either. Again, I had to manually build the site and commit the generated content to the `gh-pages` branch. The results were good, but you might have guessed it: since both experiences were _that_ similar, something did not feel quite right either.

## Casper, the friendly Ghost

Since neither the Jekyll, nor Hugo left me with a warm and fuzzy feeling, I started to doubt myself. Maybe this was crazy after all, just a fad, something my crazy overzealous perfectionism created, hunting for a solution that is perfect and 1000% right for me. So I started to re-evaluate [Ghost](https://ghost.org/). It was developed in NodeJS, is modern, relatively light-weight and is not as bloated as [WordPress](https://wordpress.org/) is nowadays.

Ghost had a successful [Kickstarter](https://www.kickstarter.com/projects/johnonolan/ghost-just-a-blogging-platform) campaign back in 2013 and was from the ground up designed for blogging – And just for blogging! It was a highly welcomed change after WordPress turned more and more into a fully-fledged CMS. Even though the focus of the project has [shifted](https://blog.ghost.org/journalism/) somewhat, I still love it and I am following their [blog](https://blog.ghost.org/) and read the [forums](https://forum.ghost.org/) regularly. I am a huge fan of their standard theme, [Casper](https://github.com/TryGhost/Casper/tree/1.4), and like [Casper 2](https://github.com/TryGhost/Casper/) even more.

The small team behind Ghost did extraordinary things already, but the project is rather young. This is a huge advantage – but also somewhat of a downside. The public API is currently read-only, there is no plugin framework, and the [marketplace](https://marketplace.ghost.org/) contains a lot of outdated or broken themes.

## So what now?!

Jekyll and Hugo are great, they have a simplicity that is unrivalled. But both have in common, that I would have to learn a completely new programming language if I ever wanted to change anything within the blogging system, or do something more complex with it. Something I neither have the time, nor the energy for. I already have enough projects and side projects. I could also not use either one out-of-the-box with GitHub, as the Jekyll theme I wanted uses unsupported gems and Go is not even a supported language for automatic deployment.

For regular blogging, I would have to build a complete workflow that either uses a Jenkins pipeline, or a self-built solution to check the new blog post in, re-generate the site and last but not least commit the contents to the `gh-pages` branch. I like the idea in theory, but I am not sure I want to put in all the work required to implement such a solution. To get a better overview of what would be required for such a solution, I decided to keep two blogs (which are currently somewhat on the back burner) on Jekyll and might re-visit such a solution in the future.

Ghost 2.0 is expected to be released this week. It will have a [new editor](https://forum.ghost.org/t/koenig-editor-beta-release/1284). Even though I rather use my [favorite Markdown Editor](https://ulysses.app/) to write my posts, I am very curious to see the new editor in action. We will see what the team will focus on after the release. I really hope it is the public API, as creating posts remotely would be big win for the platform.

For now, I think I will stick with WordPress. As much as it pains me, but I think that it is the most convenient solution. I can use Ulysses to [publish my posts](https://ulysses.app/tutorials/wordpress) to WordPress and I have a theme and plugin eco system. It is not a perfect fit, but I think it is the solution that _currently_ works best for me.
