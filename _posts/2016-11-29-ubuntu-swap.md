---
layout: post
title: Add Swap to Ubuntu
---
If you've been playing around with Elixir on small web servers, you've probably
noticed that you run out of memory building your application. An easy solution
to this problem is adding swap space to your server. Here's a quick setup guide
for Ubuntu.

The first thing we'll need to do is allocate space for our swap file.

```
  sudo fallocate -l 1G /swapfile
```

Once that's done, we'll need to enable our file, mark it, and turn it on with
these commands

```
  sudo chmod 600 /swapfile

  sudo mkswap /swapfile

  sudo swapon /swapfile
```

Once that's done, we'll want to make our swap file permanent. This way the swap
sticks around even when we reboot our server, or if it crashes.

```
  echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
