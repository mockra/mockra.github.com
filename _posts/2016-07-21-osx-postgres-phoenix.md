---
layout: post
title: OS X - Setup Postgres for Phoenix
---
Here's a quick guide for setting up postgres to work with Phoenix. The first
step is installing postgres through homebrew.

~~~
  brew install postgresql
~~~

After that's finished, you'll need to run the setup command while specifying
the utf8 encoding.

~~~
  initdb /usr/local/var/postgres -E utf8
~~~

Once that's complete you can start/restart postgres through the services command.

~~~
  brew services restart postgresql
~~~

The final step is creating your default postgres user.

~~~
   createuser -s postgres
~~~

You can now successfuly run `mix ecto.create` assuming you have the following
config in `config/devs.exs`.

~~~
  config :api, Api.Repo,
    adapter: Ecto.Adapters.Postgres,
    username: "postgres",
    database: "api_dev",
    hostname: "localhost",
    pool_size: 10
~~~

Feel free to replace the database option with something specific to your
project.
