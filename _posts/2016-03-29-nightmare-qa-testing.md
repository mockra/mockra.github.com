---
layout: post
title: QA Testing with Nightmare
---
There's a lot of tools available for doing automated browser testing, but I
recently found out about [nightmare](https://github.com/segmentio/nightmare)
and I've been pretty impressed.

Here's an example of testing with Mocha/Nightmare:

~~~
  var Nightmare = require('nightmare');
  var expect = require('chai').expect; // jshint ignore:line

  describe('test yahoo search results', function() {
    it('should find the nightmare github link first', function*() {
      var nightmare = Nightmare()
      var link = yield nightmare
        .goto('http://yahoo.com')
        .type('input[title="Search"]', 'github nightmare')
        .click('#UHSearchWeb')
        .wait('#main')
        .evaluate(function () {
          return document.querySelector('#main .searchCenterMiddle li a').href
        })
      expect(link).to.equal('https://github.com/segmentio/nightmare');
    });
  });
~~~

I've only done some basic testing so far, but I've found nightmare to be a
reliable solution for automated QA.
