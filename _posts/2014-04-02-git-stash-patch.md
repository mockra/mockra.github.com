---
layout: post
title: Git Stash --Patch
---
While working on new features, I find myself using `git stash --patch`
frequently to help isolate specific aspects of a given feature. The `--patch`
option allows you to interactively select specific changes to stash.

While you're working on a new feature that allows a user to update their
comments, and then change something in the create action. You can
stash the lines of code specific to the create action, so you can work on that
piece after finishing the update feature.

If you're liberal in your use of `git stash --patch`, you can more easily get
in the habit of making smaller and more descriptive commits as well.
