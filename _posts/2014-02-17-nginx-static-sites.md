---
layout: post
title: Static Site Hosting with Nginx
---
With a wide range of cheap hosting options, it's easy to run multiple static
sites for $5 or less. I'm currently using virtual hosts with nginx to serve
several sites from a micro instance. Here's a quick rundown on how to get
started using Ubuntu.

## Setting up Nginx

The first thing you'll need to do is install nginx.

`sudo apt-get install nginx`

We'll then want to create a directory for storing our public html files, we can
do so with the following command. Make sure to replace `yourdomain.com` with
your domain.

`sudo mkdir -p /var/www/yourdomain.com/public`

We'll also want to make sure our files are public.

`sudo chmod 755 /var/www`

The next step will be creating our virtual hosts file, which will tell nginx
how to handle our domain.

We can use the default file to get us started. Make sure to replace
`yourdomain.com` with your domain.

`sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/yourdomain.com`

We can then open our file, and update the default template with our
information.

`sudo vim /etc/nginx/sites-available/yourdomain.com`

We'll want to update the file to reflect the following:

{% gist 9062657 %}

We'll then want to create a link between the directory we're using to store our
files, and the virtual hosts directory. We can do so with the following
command, but make sure to substitute `yourdomain.com` with your domain.

`sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/yourdomain.com`

The final step for setting up our server is restarting nginx.

`sudo service nginx restart`

## Deploying Our Site

While our server is ready to serve our static website, we'll need to upload our
website to the server to start serving our content. While there are more
efficient options for deploying our static site, the simplest method is `scp`.

When running the following command, you'll want to replace `public/*` with the
directory to your static site files on your local machine, `your-directory/*`.
You'll also want to replace `username@yourdomain.com` with the your server
information.

You run the following command from your development machine.

`scp -r public/* username@yourdomain.com:/var/www/yourdomain.com/public`

This will copy the public files from our local machine to the server, so nginx
can start serving our static website.

You can repeat the steps you've just taken for any additional sites you would
like to add to the server.

## Cloudflare

An additional step we can take is setting up a CDN like
[Cloudflare](https://www.cloudflare.com). This will allow us to serve our pages
much more quickly. If you decide to use Cloudflare, you can setup a custom page
rule, and set the cache level to `Cache everything`.
