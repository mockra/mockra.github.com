---
layout: post
title: Rails Counter Cache
---
Rails offers a wide range of features that aren't commonly used, but are very
helpful in the right situation. A feature I've found useful when I need to
display an association count for a list of records is `counter_cache`.

With `counter_cache`, Rails will automatically update a column on your primary
record whenever an association is added. Given an example of a post with
comments, your Rails code will look like:

{% gist 10308296 %}

You can then use `post.comments_count` when displaying a list of posts to
increase performance and avoid unneeded queries to the database.
