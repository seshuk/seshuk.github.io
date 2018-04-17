---
layout: post
title: "Setting up jekyll"
subtitle: "My experience with it and best work-flow"
categories: ['General']
tags:
 - Personal
 - Jekyll
---

--About Jekyll

-- my experiment with jekyll on windows and mac.
-- bash on windows works with least errors.

[test]https://davidburela.wordpress.com/2017/05/17/how-to-install-jekyll-on-windows-10-with-windows-subsystem-for-linux/

**Get Ubuntu up to date and install Ruby**

```
   sudo apt-get update -y && sudo apt-get upgrade -y
```
```
   sudo apt-get install -y build-essential ruby-full
```
**update ruby gems and install Jekyll**

```
  sudo gem update –system
```
```
  sudo gem install jekyll bundler
```

```
sudo apt-get install gcc make zlib1g-dev sqlite3
sudo gem install nokogiri -v 1.6.6.2
```
-- setting up website on windows FS and access from bash.

```
bundle exec jekyll serve --watch
```