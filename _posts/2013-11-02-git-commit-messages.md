---
layout: post
title: Git Commit Messages
---
When used properly commit messages can be your most valuable source of
documentation. I find that small commits with detailed messages make it easy to
look back at past code, and see the thought process that went into writing that
code.

If I'm adding a library to my application, I can use commit messages to
document why I've decided to use this specific library and what its
functionality is. Not only is this approach helpful to other developers looking
at my pull request, it's also helpful for new developers.

Using a tool like vim-fugitive, you can easily use git blame to check commit
messages for each library in your Gemfile. If you're confused about why you're
using the flutie gem, you can check the commit that introduced that library.
