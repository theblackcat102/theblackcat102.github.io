---
keywords:
    - security
    - denyhosts
comments: true
title: Debugging deny hosts whitelist
---


For several months I am having issues connecting from my lab IP to a remote server. For months we thought the issues was caused by the crappy network backbone where we place the server. 

Lo and behold, I forgot to check denyhosts IP blacklist which I added initially for security consideration. This came up in my mind when I was going forth and back with the network admin arguing why the network is so bad. One of his reply mentioned there's no issues from nearby local server. Something clicks in my mind when I suddenly remembers the deny hosts I added few months back. Since the server can be accessed by several other users from the same lab IP, someone might just tripped the deny rule I added. 

Unsuprisingly, someone did, and after [removing all the denied hosts IP entries](https://inrg.soe.ucsc.edu/howto-unblock-an-ip-thats-been-blocked-by-denyhosts/) and added the lab IP to whitelist everything still don't work.

Hmm, perhaps it because the iptable is not updated? As mentioned in this [stackoverflow discussion](https://stackoverflow.com/questions/9225300/denyhosts-keeps-adding-back-my-ip)

A quick query of the blacklisted IP 

```
iptables -L -n -v | grep [blacklisted IP]
```

returns this

```
 3822  247K DROP       all  --  *      *       [blacklisted IP]        0.0.0.0/0
```

After droping IP the iptable firewall

```
iptables -D INPUT -s [blacklisted IP] -j DROP
```

Everything works again. This reminds me of my previous mentor always told me "never blame others before throughly verifying whether it was your fault", guess I still have a long way to go then.

