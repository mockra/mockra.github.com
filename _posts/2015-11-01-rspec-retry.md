---
layout: post
title: RSpec Retry - Fix Intermittent Feature Spec Failures
---
Once you have a set of JS based integration tests that grow large enough,
chances are that you'll run into a few tests that randomly fail. While it's
ideal to get those tests working reliably, it might not be worth the time
investment, especially if you're looking to add CI or already have one in
place.

A solution that I've found pretty helpful is adding retry to those tests, so
that one random failure doesn't fail your entire test suite on CI. The tool
I've found most useful for this is
[rspec-retry](https://github.com/NoRedInk/rspec-retry).

You can add this gem to your `Gemfile` with the following line:

~~~
  group :development, :test do
    gem 'rspec-retry'
  end
~~~

You'll also want to configure your `spec_helper.rb` to setup verbose retry.
This is important, so that you can monitor your tests and ensure that there's
not an underlying issue behind failing specs.

~~~
  require 'rspec/retry'

  RSpec.configure do |config|
    # show retry status in spec process
    config.verbose_retry = true
    # show exception that triggers a retry if verbose_retry is set to true
    config.display_try_failure_messages = true
  end
~~~

You can then flag specs that are giving you issues like this:

~~~
  it 'should randomly succeed', retry: 3 do
    expect(rand(2)).to eq(1)
  end
~~~
