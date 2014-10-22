---
layout: post
title: Soft Ether VPN
---
I've recently switched from using the OpenVPN Client/Server to Soft Ether
server with the VPN client that comes included with OS X. I've been pretty
happy with the switch so far. The OS X client is an improvement, and providing
support for more clients is always nice.

You can find a great tutorial for setting up a Soft Ether VPN server,
[here](https://www.digitalocean.com/community/tutorials/how-to-setup-a-multi-protocol-vpn-server-using-softether).

Once your server is configured, setting up your client is a walk in the park.
You simply need to open up your network preferences, and add a new service.
You'll want to select the following options:

`Interface: VPN`

`VPN Type: L2TP over IPSec`

`Service Name: Whatever you want`

Once you've created the new service, you'll need to enter your server's IP
address and the account name that you setup. You'll also need to click on
`Authentication Settings`, and enter the credentials you setup when installing
and configuring the server.

You can then go to the advanced settings page, and select the options you need.
I would recommend sending all traffic over the VPN connection. You'll also want
to show the VPN status in the menu bar.

Once you've finished configuring your service, you can connect to your VPN
server through the menu bar icon.
