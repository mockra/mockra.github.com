---
layout: post
title: Web Scraping in Node with Cheerio
---
If you're looking to write a simple bot or script that does web scraping, then
node might be a great option. The cheerio library makes it easy to work with
HTML. Here's a quick example:

~~~
  npm install request --save
  npm install cheerio --save
~~~

Here's a sample script for parsing article information from a list:

~~~
  request(articleListUrl, async function (err, resp, body) {
    const $ = cheerio.load(body)

    const article = $('ul#articles-list li.article:first-of-type')
    const articleLink = article.find('.media-body a:first-of-type')

    const articleTitle = articleLink.text()
    const articlePath = articleLink.attr('href')
  })
~~~

It's surprising how well the jQuery API lends itself to web scraping.
