---
layout: post
title: Git Hosting
---
While I'm a big fan of many of the hosting services out there for git
repositories, it's nice to be able to provide your own server. Here's a quick
rundown on setting up a git server.

If you don't already have git installed, you'll need to do so. If you're
running a Ubuntu machine, you can do so with the following commands:

```
  sudo apt-get update
  sudo apt-get install git
```

The first thing you'll want to do after installing git is setup a `git` user:

```
  sudo useradd -m -d /var/git -s /bin/bash -c 'Git' git
  sudo su - git
```

The next step is setting up SSH keys for your users:

```
  mkdir /var/git/.ssh
  touch /var/git/.ssh/authorized_keys
  chmod 700 /var/git/.ssh
```

You'll then want to add the public keys of your users to the
`/var/git/.ssh/authorized_keys` file.

After you've provided SSH access for your users, you can start adding projects.

```
  mkdir your-project.git
  cd your-project.git
  git init --bare
```

Once you've setup the bare git repository on your server, you can add it to
your local git repository.

```
  git remote add origin git@git.yourserver.com:your-project.git
```

Once you've added your new remote repository, you're all set, and can continue
using git as you're used to.
