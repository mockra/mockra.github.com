---
layout: post
title: Deploying with Ember-Cli-Deploy
---
There's a lot of different approaches to deploying your ember application, and
it's an interesting discussion. I personally like the approach of keeping your
client and server deploys completely separate. Primarily deploying your EmberJS
client code directly to a CDN. This alleviates a lot of scaling concerns, since
you now only need to focus on scaling your API. It also has the benefit of
speeding up your application's delivery.

One of the tools I use for my deploys is
[ember-cli-deploy](http://ember-cli.github.io/ember-cli-deploy/). It's based on
a lightning fast deploy philosophy, and is built around using adapters for your
specific deployment strategy.

I use Amazon Cloudfront to serve my EmberJS applications from s3. For that
approach I use the
[ember-deploy-s3](https://github.com/LevelbossMike/ember-deploy-s3) and
[ember-deploy-s3-index](https://github.com/Kerry350/ember-deploy-s3-index)
adapters.

Once you've configured ember-cli-deploy with the right adapters for your
configuration, you have access to several commands that make deploying a
breeze.

You can use `ember deploy --enviornment production` to upload your current
build. Once your build has been deployed, you can activate that build through
the following command:

```
  ember deploy:activate --revision your-revision-id --environment production
```

If for some reason you need to rollback to a previous build, you can check your
previous releases with:

```
  ember deploy:list --environment production
```

Once you've found the release you want to rollback to, you can simply activate
that release.

I've been very happy with this approach so far, since it allows me to very
quickly deploy my client builds. It also takes a lot of the scaling concerns
out of my hands, since Cloudfront takes care of a lot of those issues for me.
One of the few hiccups is handling non-fingerprinted assets served through
Cloudfront, which will need to be invalidated as part of the deploy process.
