---
layout: post
title: "Setting up jekyll"
subtitle: "My experience with it and best work-flow"
categories: ['General']
tags:
 - Personal
 - Jekyll
---

### Jekyll:
 Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. Jekyll is the engine behind GitHub Pages, which you can use to host sites right from your GitHub repositories.

 The great thing about Github pages is that the simplicity which is ideal for blogs because it makes it easy to focus of the content, rather than keep trying to setup stuff. There are lot of nice themes out there that are open source and very easy as well as free to use. This is one of the main reasons that I'm sticking to this platform for a while.

 I have had some difficulty setting up my theme and website on both Windows and Mac OSx, I had to spend lot of hours setting up my local dev version of the blog.

 Enter _Bash on Ubuntu on Window_. From my research I realized that setting up jekyll is much easier on unix like environments ( in my experience it failed multiple time on my work Mac book pro). I tried setting up jekyll on Unix subsystem on Windows.

 I have to admit it was cool experience below are the steps/commands I had to use on bash:

- ***Gets Ubuntu up to date and installs Ruby:***

```
   sudo apt-get update -y && sudo apt-get upgrade -y
```
```
   sudo apt-get install -y build-essential ruby-full
```

- ***Update ruby gems and install Jekyll:***

```
  sudo gem update –system
```
```
  sudo gem install jekyll bundler
```

The only error I got was while it was unable to install nokogiri gem that was needed for my website. I used following to fix that and everything else worked like a charm.

```
sudo apt-get install gcc make zlib1g-dev sqlite3
sudo gem install nokogiri -v 1.6.6.2
```

Once bundler installs all the dependencies following command can be used to start the website on local host. And off you go with your local dev site.


```
bundle exec jekyll serve --watch
```


The cool thing with --watch switch is it track changes on real time and automatically builds the site on any changes, making it super easy to update using editors like VS Code.

I create a bash session on the terminal window in VS Code and its a seem less experience. 

One thing to keep in mind is to clone you website on Windows file system instead of unix one. That way the change can be done using VS Code or Sublime etc.
