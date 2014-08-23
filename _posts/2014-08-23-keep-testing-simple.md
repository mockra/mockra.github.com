---
layout: post
title: Keep Testing Simple
---
When I first got into programming, I decided to teach myself Ruby on Rails. One
of the things that I struggled the most with early on was testing. While I
picked up programming concepts and simple features fairly smoothly, I had a
very difficult time figuring out how to write tests.

It was until I started thinking about why I was struggling so much specifically
with testing that I was able to progress. The problem was my mindset when
sitting down to write a test.

While writing the code for a comment system, I knew what the outcome was
supposed to be, so it was easy to break it down into small steps to achieve
that outcome. For some reason when writing tests, I was focusing on what the
test code was supposed to be for the feature code I wanted to write or had
written.

This realization made me focus on what the outcome was supposed to be for the
method or feature under test. I could then create the steps necessary to reach
that outcome in my tests. Here's a simple feature spec as an example:

{% gist mockra/e26634d38eaaceeab712 %}

In this example the outcome we're looking for is authenticating a user, and
having his details displayed on the page. When we start with that goal in mind,
writing our test becomes much simpler.

In order for a user to log into our system, he needs to have an account. Our
first step then becomes creating a user for our feature spec. Now that we have
our first step, we can ask Google a simple question, such as, `creating a model
in rails for testing`. This will then lead us to setup fixtures using the
default stack, or setting up something like FactoryGirl or Miniskirt.

Once that's done, we can move onto the next step in our process. For a user to
login into their existing account, they'll need to visit the login page.
Another Google search will lead us to the `visit` method, which solves the next
step in our login test.

From there, we can continue down this path to get the user to fill in his
login details, and then submit them. Which solves our original goal of
expecting his login details to be displayed on the user section of our page.

By focusing on the outcome we want, it's much easier to create the small and
often simple steps necessary to reach that outcome. This is an important
mindset to have not just for testing, but programming in general.

When learning a new programming language or tool set, I've found it's important
to remember the basics of programming when it comes to testing. It's too easy
with testing to focus on the right way to write a test, or what method you're
supposed to use. The correct way to write tests is the same way you write your
programs. Find the outcome you want, and focus on the small steps necessary to
reach that outcome.
