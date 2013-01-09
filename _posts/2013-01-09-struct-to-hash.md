---
layout: post
title: Struct to Hash
---
I've been using Structs a lot lately, and recently needed to convert a Struct to
a Hash. It's a very simple process, and something that I'm sure I'll use often.

    Article = Struct.new :title, :text

    essay = Article.new 'Poem', 'Roses are Red'
    # #<struct Article title="Poem", text="Roses are Red">

    Hash[essay.each_pair.to_a]
    # {:title=>"Poem", :text=>"Roses are Red"}

Another cool thing I picked up was how to use map with indexes.

    articles.each_with_index.map {
      |article, index| article.title = title_array[index]
    }
