# Yummy Jekyll Theme

[Live Demo](http://dongchuan.github.io/)

## Notable Features

* Compatible with Jekyll 3.x and GitHub Pages
* Based on Bootstrap
* [Github Module](http://dongchuan.github.io/open-source) to show your popular projects in a single page and on sidebar automatically. (Datas are retreived by github metadata instead of by api calls, so no delay) 
* [Post Module](http://dongchuan.github.io/blog) to show all your posts with timeline
* [Bookmark Module](http://dongchuan.github.io/bookmark) to establish a quick mark about all libs/tools/books you like to use.
* [Post Navigation Module](http://dongchuan.github.io/css/2016/04/22/CSS-Animation.html) to generat a quick directory of your post by titles/subtitles automatically.
* Support [Disqus Comment](https://disqus.com/home/explore/)
* Support [Google Analytics](https://analytics.google.com/analytics/web/)

Features in feature:
* A Footprint module to show all your travel around the world

## Install and setup

Before using it, you may need [Bower](http://bower.io/) and [Bundler](http://bundler.io/) on your local to install dependencies.

> When install dependencies by bundler, you could have problem about installing json. Check response of [Massimo Fazzolari on Stackoverflow](http://stackoverflow.com/questions/8100891/the-json-native-gem-requires-installed-build-tools) to quick fix your problem. (Please also use latest version instead of 1.9.3 mentioned in the response)

1. Fork code and clone
2. Run `bower install` to install all dependencies in [bower.json](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/bower.json)
3. Run `bundle install` to install all dependencies in [Gemfile](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/Gemfile)
4. Update `_config.yml` with your own settings.
5. Add posts in `/_posts`
6. Commit to your own Username.github.io repository.
7. Then come back to star this theme!

> For the moment, when you test on your local, you need to keep internet connection. Bug will be fixed soon.

## How to use

### [Post Navigation Module](http://dongchuan.github.io/css/2016/04/22/CSS-Animation.html)

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

For example, post [CSS Animation](https://github.com/DONGChuan/DONGChuan.github.io/edit/master/_posts/2016-04-22-CSS-Animation.md)


### [Bookmark Module](http://dongchuan.github.io/bookmark)

To add new marks, you only need to edit [bookmark.md](https://github.com/DONGChuan/Yummy-Jekyll/blob/master/bookmark.md).

## ToDo

- [ ] Support favicon
- [ ] List posts by a specified tag
- [ ] New module FootPrint to show your world around trips
- [ ] Show projects from your orgnization on github. (Siderbar, in open-source page)
- [ ] To fix bug - could only test on local with internet connected.

## License

The Apache License 2.0

Copyright (c) 2016 DONG Chuan

Check [LICENSE](https://github.com/DONGChuan/DONGChuan.github.io/blob/master/LICENSE) file and [official website](http://www.apache.org/licenses/LICENSE-2.0) for details
