---
layout: post
title:  How to create a blog using Github Pages
date: 2020-03-08 19:37:20 +0300
description: Create a blog using Jekyll and Github Pages.
img: blog-frontpage.png # Add image post (optional)
fig-caption: Blog's frontpage # Add figcaption (optional)
tags: [Blogging]
comments: true
---
How to quickly setup a blog using Jekyll Github Pages with bonus tracks for comments and analytics.

My first blog post! I’ve been trying to commit to blogging for a while with very little success. Created a few blogs that ended up with exactly one post. Hope this time it sticks. I always thought a blog as a powerful tool. It allows to share thoughts and experiences but, more importantly, it's a log for your journey.

I like simple tools and my requirements for a blog are:

- Use the same tools I know and like for writing and versioning.
- Easy to setup.
- Use my own domain name.
- People can provide feedback.
- Track user activity. Just to annoy privacy conscious people.

I spend a couple of hours researching and came up with the following toolset:

- [Jekyll][jekyll]: a simple publishing tool to manage posts in [Markdown][markdown] files. You can test them locally.
- [Git][git]: a welcomed side effect of content being just files.
- [Github Pages][gp]: perfect integration with Jekyll and Git.
- [Disqus][disqus]: simple way to add discussions.
- [Google Analytics][ga]: common solution to the activity tracking issue.

What follows is the step-by-step process I followed.

__DISCLAIMER__: I don’t have any affiliation with the tools and services mentioned in this post. I just mention them to describe the process I went through.

## Install Jekyll
There are many ways to install [Jekyll][jekyll] but I went with the quick and dirty:

    sudo gem install jekyll

## Register domain name
I feel like I’m stating the obvious here but, if you want your own domain name, you need to register it. I’ve been managing my domains with GoDaddy for a while so it was the obvious option.

If you don’t want your own domain, you can use the default domain name for your Github user page. Example: _esancho.github.io_

## Find a theme you like
I think you will appreciate using a theme for two reasons:

- Aesthetics
- Themes usually support some of the features you might want (ie: Google Analytics)

There are plenty of themes at [Jekyll Themes][jt] and I chose [Harmony][harmony].

## Create repository for Github Pages
You have a few options here depending if you’re using the default or a custom Jekyll theme.
Using [Harmony][], the easiest way to start is to:

- Fork the theme repository to your account. In my case, I forked https://github.com/gayanvirajith/harmony as https://github.com/esancho/harmony
- Rename repository so Github Pages can you use it. It needs to respect the pattern _USERNAME.github.io_. I renamed it as esancho.github.io

## Configure basic settings
Clone repository (change repository name with your own):

    git clone https://github.com/esancho/esancho.github.io
    cd esancho.github.io

Modify Jekyll’s config file (_config.xml). You will need to at least modify the url and baseurl settings.

Test your changes locally. Easiest way is to serve files with Jekyll’s built-in web server

    jekyll serve

Now you can access your website at: [http://127.0.0.1:4000](http://127.0.0.1:4000)

## Test your live site
You just need to push your changes for your website to be functional using the default Github Page domain name.

    git add —all
    git commit -m “Applying basic config changes”
    git push

You should now be able to access your live website with your browser, using a URL like: [http://esancho.github.io](http://esancho.github.io)

## Configure Github Pages to use your domain name

This is a pretty straightforward step. You just need to create a  file named CNAME in your repository’s root. The only content of the file is a single line with the domain name you want to use (and already registered).

Example for my website:

    estebansancho.com

## Setup DNS

This step will vary depending on your name registrar and DNS hosting but you need to follow the steps described here: [https://help.github.com/articles/setting-up-an-apex-domain/](https://help.github.com/articles/setting-up-an-apex-domain/)

To keep it simple, you need to add two A records records that point your custom domain to the following IP addresses:

- 192.30.252.153
- 192.30.252.154

In my case with GoDaddy, my DNS settings for estebansancho.com are:

![]({{ '/img/go-daddy-dns.png' | prepend: site.baseurl | prepend: site.url }})

## Add Discus comments
1. Sign-up on [Disqus][].
2. Configure your website at [Disqus][].
3. Configure Jekyll to use Disqus

This process is documented here [https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions](https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions) but there’s an error in step 2.

{% raw %}
Instead of:

    {% if post.comments %}

It should read:

    {% if page.comments %}

{% endraw %}

## Google analytics
I chose the [Harmony][] theme partially because it supports Google Analytics. So I only needed to:

1. Sign-up for [Google Analytics][ga]
2. Create a Property in [Google Analytics][ga]
3. Configure Tracking Id (UA-XXXXXXXX-X) in the _config.yml file (google_analytics_key).

## Conclusion
I was able to setup my blog in a couple of hours with the tools described here. I’m very happy wth the results and don’t have any excuses now to avoid writing.
I will try to cover the tools I use for writing in an upcoming post.

[jekyll]:    http://jekyllrb.com
[git]: https://git-scm.com
[markdown]: http://daringfireball.net/projects/markdown/
[gp]: http://pages.github.com/
[disqus]: https://disqus.com
[ga]: https://analytics.google.com/
[jt]: http://jekyllthemes.org/
[harmony]: http://jekyllthemes.org/themes/harmony/