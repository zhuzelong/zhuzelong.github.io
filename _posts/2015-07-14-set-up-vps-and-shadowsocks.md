---
layout: post
title: Set up VPS and Shadowsocks
categories: [Record]
tags: [vps]
published: True

---
## Set up VPS

### VPS Suppliers

Github offered a Student Pack including a coupon for DigitalOcean (DO), so I set up a VPS on DO.


### Setting up

The tutorials given by DO are useful:

- [initial setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7?utm_source=Customerio&utm_medium=Email_Internal&utm_campaign=Email_CentOSDistroApacheWelcome)
- [connect to VPS via SSH](https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh?utm_source=Customerio&utm_medium=Email_Internal&utm_campaign=Email_CentOSDistroApacheWelcome)
- [security guide](https://www.digitalocean.com/community/tutorials/7-security-measures-to-protect-your-servers?utm_source=Customerio&utm_medium=Email_Internal&utm_campaign=Email_CentOSDistroApacheWelcome)

It took me a while to configure SSH login. It should be noted that the permission of `~/.ssh/` and `~/.ssh/authorized_keys` should be set properly.


### iptables

CentOS 7 replaces `iptables` with `firewalld` but one can still enable `iptables`. See [here](http://stackoverflow.com/questions/24756240/how-can-i-use-iptables-on-centos-7) for details.


## Shadowsocks

[This tutorial](https://plus.google.com/103234343779069345365/posts/Xce4EJpLGhX) is in detail and updated. One of the issues worth noting is that install `M2Crypto` by `yum install m2crypto` would not incur errors.
