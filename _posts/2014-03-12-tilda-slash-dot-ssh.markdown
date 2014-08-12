---
layout: post
title: "Tilda slash dot ssh"
date: 2014-03-26 10:08:07
tags:
- ssh
- config
---

I think it out loud all the time as I type it -- maybe I even say it?

  *vi ~/.ssh/config*

It's made my life so much easier the last few months. A bunch of assets I need to ssh to, but none accept my local user's ssh key. Worse, they all accept different ssh keys. Sure, I have the keys they want, and can

    ssh -i /path/to/the_key.pem theuser@10.10.10.10

...but that's a PITA to type over and over. So, *vi ~/.ssh/config* to the rescue!


    Host headless
      User theuser
      Hostname 10.10.10.10
      IdentityFile /path/to/the_key.pem


Put something like that into ~/.ssh/config, and now you can

    ssh headless

Boom! It's easy; it's power. So the question at this point is bound to be, why not simply do this?

    cat ~/.ssh/id_rsa.pub | ssh -i /path/to/the_key.pem \
    theuser@10.10.10.10 'cat >> .ssh/authorized_keys'

Well, sometimes I just don't want to do that.