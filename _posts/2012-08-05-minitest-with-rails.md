---
layout: post
title: Minitest with Rails
---

<p>I&#8217;ve been using Minitest in a small project I&#8217;ve been working on lately. I really like the assert syntax and feel it&#8217;s a lot cleaner than spec. Here&#8217;s my test_helper.rb file, as well as an example controller test.</p>

{% gist 3266145 %}

<p>Right now I&#8217;m using Miniskirt for my factories and I can&#8217;t say I&#8217;m missing any of the FactoryGirl features that aren&#8217;t included in Miniskirt. I&#8217;m also using Capybara for integration testing, as well as Turn for test output.</p>
