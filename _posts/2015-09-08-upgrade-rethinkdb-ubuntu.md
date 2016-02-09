---
layout: post
title: Ubuntu - Upgrade RethinkDB
---
Upgrading your RethinkDB server is pretty straightforward these days now that
you don't need to migrate your data manually. Here's a list of commands you'll
need to run:

~~~
  sudo apt-get update
  sudo apt-get upgrade rethinkdb
  rethinkdb index-rebuild -a authKey
~~~

You'll need to replace `authKey` with your database authentication key.

I'd also recommend doing a quick backup in case anything goes wrong with the
update. You can do so by running:

~~~
  rethinkdb dump
~~~
