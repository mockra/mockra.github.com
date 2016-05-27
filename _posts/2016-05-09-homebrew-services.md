---
layout: post
title: Homebrew Services
---
If you're like me, you likely have a long list of homebrew packages installed.
You most likely also have quite a few running through `launchd`. Starting,
stopping, and restarting these packages has likely been a cumbersome process.
Luckily, there's an easy solution to your problem in Homebrew Services.

You can install homebrew services by running:

~~~
  brew tap homebrew/services
~~~

The first thing you'll want to do from there is see a list of currently running
services, which can be done by running:

~~~
  brew services list
~~~

Here's an example of the ouput:

~~~
  mysql        stopped
  postgresql   started username LaunchAgents/homebrew.mxcl.postgresql.plist
  redis        started username LaunchAgents/homebrew.mxcl.redis.plist
  rethinkdb    stopped
~~~

Now that I have homebrew service, I can start `mysql` by running:

~~~
  brew services start mysql
~~~

If I wanted to stop running `redis`, I could do that with:

~~~
  brew services stop redis
~~~

Homebrew services also comes with a handy utility for cleaning up stale
services and unused plists.

~~~
  brew services cleanup
~~~
