---
layout: post
title: RethinkDB CSV Exports
---
I've been writing some toy scripts recently that use RethinkDB as a data store.
I've gotten a couple of requests to export the data to a CSV document for
manipulation in excel. Luckily, there's an easy way to export your data using
the `rethinkdb` command line tool.

~~~
  rethinkdb export -e dbname.posts --format csv --fields title,author
~~~

This command allows you to specify a csv or json format for the export. You'll
then need to pass in the database and table you want to export. The fields
option allows you to pass in the fields you wish to export.
