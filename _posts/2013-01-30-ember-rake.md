---
layout: post
title: Ember Rake
---
I've been finding myself updating my ember build pretty frequently, so I
decided to write a small rake task for updating to the latest build.

The script will clone the ember and ember-data repositories to ~/.ember and
~/.ember-data. The files are then placed in vendor/assets/javascripts in
relation to your current directory.

The script copies the unminified versions, so you'll need to alter it if you
want the minified builds.

You can find the script [here](https://gist.github.com/4679199).
