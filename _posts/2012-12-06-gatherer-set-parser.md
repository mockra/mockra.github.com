---
layout: post
title: gatherer_set_parser
---
A couple of days ago, I released an MTG parser I wrote for a small side project.
The gem takes a set name as input and will return an array of card hashes. The
tool does this by parsing the MTG Gatherer website.

It's the first project of this type that I've worked on, and I would greatly
appreciate feedback. I know there's a much more elegant method of formatting
strings than simply chaining gsub methods.

I've personally been using it with more recent sets, but it has been tested
against a number of older sets, and should be pretty robust. If you find any
issues with specific sets or cards, please submit an issue to the project and
I'll gladly fix it.

If there are enough people that show interest, I'll consider downloading all of
the sets to a server and creating an API. You can check out the project on
[github](https://github.com/mockra/gatherer_set_parser).
