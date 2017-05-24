---
layout: post
title:  Ruby Gems and Windows
date:   2017-05-24 01:03:38 +0000
---


> "Why the heck whould you do this?" - 95% of programmers

I know that you may think I am the odd one out in the programmer community when I say that I use Redmond's prized modern operating system. However, it would seem that 41% of programmers aggree with me (according to stackoverflow). While Microsoft slowly caves in and gives us bash, peice by precious peice. I thought I would document my experiance building a Ruby Gem and shipping it on Redmons very own pride and joy.

## Installing Ruby, Bundle...
To write ruby we will need a ruby interpretor. I got mine [here](https://rubyinstaller.org/downloads/) but feel free to use which ever one you like.

Make sure the installer adds it to the path (or do it yourself) and then you have all that you need. just be sure to run `gem install bundler` to make your dependencies sane. Also we will need it later.

## Creating, Building and Pushing a Gem
This step is simple enough really, just run `bundle gem <gem_name>` and give your life to the MIT licence, now and forever, and you should be doing great!

In order to build it you will have to edit the following configs in the `project-name.gemspec` file

1. `spec.summary`
2. `spec.description`
3. `spec.homepage (http://rubygems.org/gems/<project name>)`

then to build it is `gem build <project_name>.rspec` and to push is `gem push <project_name>-<version_number>.gem`

Now here is the fun part.

### Loading executables

Since this is windows and we insist on backwords compatibilty we just have to look in the wrong place for these. By default Gem will look in `<project root>/exe/` but our files are in `<project root>/bin/` (Or they should be anyway) and running `spec.executables << '<file_name>'` will therefor look in the wrong place. Don't worry, all you need to do is add `../bin/<file_name` to your `spec.executables` with a D---(] (shovel, or `<<` in ruby) and it will build and run just fine.

## Notes:
Do not include standard libs (like `open-uri` in the gemspec or ruby will crash for some reason.)


