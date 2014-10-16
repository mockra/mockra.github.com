---
layout: post
title: Node Script Monitoring with Forever
---
One of the tools I use to keep long running processes running in node is
[forever](https://github.com/nodejitsu/forever). Forever is a CLI tool that
ensures a given script keeps running, as well as providing additional
functionality.

I typically use forever to manage a variety of small node scripts and bots I
run off of one of my servers. One of the nice things about forever is how
simple it is to use. Starting up a new script is as simple as `forever start
your-script.js`.

When something goes wrong with one of your scripts, you can run `forever list`
to pull up a list of scripts you're monitoring. This will also include the path
of the corresponding log file, so you can quickly pull up the log for that
specific script.

Restarting and stopping scripts is incredibly easy as well, which makes quickly
updating your scripts painless. Overall, the best part about `forever` is that
it just works. It's been running a bot of mine without any issues for almost a
year now, as well as other scripts for a shorter period of time.
