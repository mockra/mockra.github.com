---
layout: post
title: Loudred Twitter Bot
---
I recently created a twitter bot in node.js as a fun little side project. While
fairly simple, I've found the bot to be pretty helpful when it comes to
minimizing the amount of websites I visit for news.

The bot grabs the latest top 3 posts from various subreddits I follow, and
posts them to Twitter. I'm a big fan of using Twitter as a form of content
curation, and this eliminates another news source I used to visit.

![loudred stream](/images/loudred_twitter.png)

The bot uses the [twit](https://github.com/ttezel/twit) library for interacting
with the Twitter API, but I ended up writing my own library for fetching posts
from Reddit.

You can checkout the code for this bot on
[Github](https://github.com/mockra/loudred), and visit the bot on
[Twitter](https://twitter.com/loudred_).
