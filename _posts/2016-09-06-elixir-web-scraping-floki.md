---
layout: post
title: Elixir Web Scraping with Floki
---
One thing I end up working with in all languages is the ability to scrape data
from a web page. I've been pretty happy with the tools available in Elixir for
doing so, here's a quick preview.

In this snippet, we're going to be crawling my personal blog using
[HTTPoison](https://github.com/edgurgel/httpoison) and
[Floki](https://github.com/philss/floki).

```
  posts = "https://www.mockra.com"

  body = HTTPoison.get!(index_url, [], hackney: [:insecure]).body

  posts = Floki.find(index_body, "section.post")
```

You'll quickly notice something strange about the options we're passing to
HTTPoison. I've run into an issue when crawling some websites due to a bad
certificate, so this is a work around for now. You can find more details about
the issue [here](https://github.com/benoitc/hackney/issues/240).

Once we get the content body, we can pass it into Floki to search for the information we want. In this example we're grabbing the posts on the index page. If we wanted to get the title of the first post, we could do so with:

```
  posts
  |> List.first
  |> Floki.raw_html
  |> Floki.find("h3")
  |> Floki.text
```

This is a bit of a crude example, but in this case, we're grabbing the first
post from the list and converting it back to html. This lets us use the find
function again to grab the h3 element for the post. We then use `Floki.text` to
get the post title.
