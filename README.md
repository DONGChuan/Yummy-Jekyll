# Yummy Jekyll Theme

A Simple, Bootstrap Based Theme. Especially for developers who like to show their projects on website and like to take notes. There are also some magical features to discover. 

## [Live Demo](http://dongchuan.github.io/)

Open issues if you find bugs or even have trouble installing jekyll or dependencies. :D

Or contact: dongchuan55@gmail.com

> Strongly suggest to fork and change project name to create your GitHub Pages instead of downloading it directly. Because in the future, I will develop many funny modules like 'footprint' to show your world wide trip. Could be easier to merge new features in the future.

## Notable Features

* Compatible with Jekyll 3.x and GitHub Pages
* Based on Bootstrap
* [Github Module](http://dongchuan.github.io/open-source) to show your popular projects in a single page and on sidebar automatically. (Datas are retreived by github metadata instead of by api calls, so no delay) 
* [Post Module](http://dongchuan.github.io/blog) to show all your posts with timeline
* [Bookmark Module](http://dongchuan.github.io/bookmark) to establish a quick mark about all libs/tools/books you like to use.
* [Post Navigation Module](http://dongchuan.github.io/css/2016/04/22/CSS-Animation.html) to generat a quick directory of your post by titles/subtitles automatically.
* Support [Disqus Comment](https://disqus.com/home/explore/)
* Support [Google Analytics](https://analytics.google.com/analytics/web/)

Features in future:
* A Footprint module to show all your travel around the world
* Feature to share. (Facebook, twitter, evernote and so on)
* (Not sure) A embeded todo list. (Not sure) to travel, to complete, to do for your parents, etc. To do in life!
* Creative ideas to discuss with you :P

## Install and setup

Before using it, you may need [Bower](http://bower.io/) and [Bundler](http://bundler.io/) on your local to install dependencies.

1. Fork code and clone
2. Run `bower install` to install all dependencies in [bower.json](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/bower.json)
3. Run `bundle install` to install all dependencies in [Gemfile](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/Gemfile)
4. Update `_config.yml` with your own settings.
5. Add posts in `/_posts`
6. Commit to your own Username.github.io repository.
7. Then come back to star this theme!

> When install dependencies by bundler or gem, you may have some errors depending on your environment.

> Error about `json`. Check response of [Massimo Fazzolari on Stackoverflow](http://stackoverflow.com/questions/8100891/the-json-native-gem-requires-installed-build-tools) to quick fix your problem. (Please also use latest version instead of 1.9.3 mentioned in the response)
  
> Error about `jekyll-paginate`. Please check [here](http://stackoverflow.com/questions/35401566/dont-have-jekyll-paginate-or-one-of-its-dependencies-installed)

> Error about `SSL_connect`. Please check [here](http://stackoverflow.com/questions/15305350/gem-install-fails-with-openssl-failure) and [here](http://railsapps.github.io/openssl-certificate-verify-failed.html)

> For the moment, when you test on your local, you need to keep internet connection. Bug will be fixed soon.

## How to use

#### Create a new post

Create a `.md` file inside `_posts` folder.

Name the file according to the standard jekyll format.

```
2016-01-19-i-love-yummy.md
```

Write the Front Matter and content in the file.

```
---
layout: post
title: Post title
category: Category
tags: [tag1, tag2]
---
```

Please find examples [here](https://github.com/DONGChuan/DONGChuan.github.io/tree/master/_posts)

> Jekyll supports different structure of repository. You could just create as many folders as you want under _posts. Then jekyll will look through all folders/subfolders to find your posts. So cool, right? :D

#### [Post Navigation Module](http://dongchuan.github.io/css/2016/04/22/CSS-Animation.html)

When writing post, please always follow this format:

```
Description about this post, blablabla

## Title A

### Title A-1

### Title A-2

## Title B

### Title B-1

```

So, Title A, A-1, A-2, Title B, B-1 will be detected and created as a directory

For example, [a demo post](https://github.com/DONGChuan/DONGChuan.github.io/edit/master/_posts/2016-04-22-CSS-Animation.md)

But if you do not like it or your post is quite short. You want to hide this navigation to make your post occupy your full screen. You just need to set **no-post-nav:true** in the Front Matter of the post where you want to hide this feature :D

#### [Github Module](http://dongchuan.github.io/open-source)

This module will get automatically all your repository information from github. But to test on your local, you must keep internet connection. 
In the future, it will also show the repositories you contributed a lot and the ones of your organization.

#### [Bookmark Module](http://dongchuan.github.io/bookmark)

To add new marks, you only need to edit [bookmark.md](https://github.com/DONGChuan/Yummy-Jekyll/blob/master/bookmark.md).

#### [Customize About Page](http://dongchuan.github.io/about)

Feel free to customize about.me page to show yourself. You only need to modify [about.md](https://github.com/DONGChuan/Yummy-Jekyll/blob/master/about.md) and [about.html](https://github.com/DONGChuan/Yummy-Jekyll/blob/master/_includes/about.html)

## ToDo

- [ ] List posts by a specified tag
- [ ] New module FootPrint to show your world around trips
- [ ] Show projects from your orgnization on github. (Siderbar, in open-source page)
- [ ] To fix bug - could only test on local with internet connected.

## Contributor

* [DONGChuan](https://github.com/DONGChuan)
* [Mojtaba Koosej](https://github.com/mkoosej)
* [shahsaurabh0605](https://github.com/shahsaurabh0605)
* [Z-Beatles](http://www.waynechu.cn/)
* [LM450N](https://github.com/LM450N)

## License

The Apache License 2.0

Copyright (c) 2016 DONG Chuan

Check [LICENSE](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/LICENSE) file and [official website](http://www.apache.org/licenses/LICENSE-2.0) for details
