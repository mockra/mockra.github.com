---
layout: post
title: Benefits of Pairing
---
A common misconception I've found in regards to pairing is that it's mostly done to improve code quality. While that's certainly one of the many benefits, I think the most important benefits are related to culture and knowledge sharing.

### Culture

One of the more difficult tasks for an engineering manager is building a shared culture among the team. Pairing is one of the best tools for accomplishing this goal. An easy example would be if you're looking to establish TDD as a common practice.

It's one thing to tell your developers to use TDD and even give a demonstration of its benefits, but if you want to ensure they're following it, the best way is to pair with them. If you're pairing on a regular basis and test drive all of the features while pairing, the other developers will start to adopt TDD and even bring new developers up to speed when pairing with them.

You've now established a culture of using TDD that will continue even if you stop pairing with your developers. The practice of pairing will ensure that your developers that use TDD currently will instill that habit upon new team members.

### Knowledge Sharing

One of the many issues a growing team will encounter is the concept of isolated knowledge. If only one person knows how the new billing system works, product managers, engineers, and stake holders will all need to go to that one person with questions.

One of the best ways to mitigate this issue is through pairing. If you establish a culture of pairing, you'll at a minimum have at least two people with knowledge of any given feature. This also allows for healthy discussion between engineers when it comes to building out new functionality around those features. It will also help drive discussion when it comes to grooming or estimating stories.

If your team is in the habit of rotating pairs, pretty soon your entire team will have a good idea of how each feature works. Your engineers will no longer get calls while on vacation, because anyone on the team is capable of answering those questions.

### Getting Started

Introducing pairing to your team can be a challenge depending on your engineers. A lot of developers can be pretty averse to the idea of pairing if they don't have experience with it. I think slowly introducting the concept is the right approach, as well as keeping it optional for each team.

A low barrier option to introduce pairing is by forcing code reviews to be a process that requires a pair. Paired code reviews are a great practice in general, because it's a lot easier to relate to the original author when you're talking to them while reviewing. This helps avoid some of the tensions that can arise through text based reviews. It will also help lower cycle time, because engineers need to actively seek a reviewer.

Once developers are in the habit of pairing for code reviews, you can start marking stories or features as items that need to be paired on. More complex stories or ones with a lot of stake holders are great use cases for pairing. Pairing on those stories will help with knowledge share, and get developers used to the idea of pairing.

I've found that once the ball starts rolling on pairing, engineers will usually jump on pretty quickly.

### Tools

[ScreenHero](https://screenhero.com/) will allow you to share your entire screen with your pair and provides voice chat. This is useful for paired code reviews which require a browser typically, as well as for when developers switch to a browser while working on a feature.

[Tmate](https://tmate.io/) is another great option, but has limitations for code review, as well as feature work that can't be done in the terminal. You'll also need a way to communicate with your pair. I've found [Discord](https://discordapp.com/) to be a great option there.