---
layout: post
title: Scheduled Tasks with Elixir
---
I've been writing several bots and scripts using Elixir lately, and I've found
it to be a pretty great option. One of the key tools I've been using is the
[quantum-elixir](https://github.com/c-rack/quantum-elixir) library.

If you've ever used cronjobs before, quantum provides the same type of
functionality. You can setup scheduled tasks to run at specific intervals
through your config file. Here's an example `config/config.exs` file:

```
  config :quantum, cron: [
    # Every 2 minutes
    "*/2 * * * *": {Mockra.Bot, :run},
  ]
```

In this example, the run function on my bot module will run every 2 minutes.

Once I've setup my script and config, I'll use mix to run my script. I'll use
the following command in a tmux session:

```
  MIX_ENV=prod mix run --no-halt
```

I've transferred a few ruby and node scripts to Elixir, and the droplet I use
for scripts has dropped from ~85% CPU load to ~1.5%. These are all unoptimized,
but I was pretty surprised by the results.
