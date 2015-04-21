---

layout:			default
title:  		Cisco Cheatsheet
type:			  post
navigation: false

date:   		2015-02-12
excerpt: 		Useful things to know for managing Cisco devices
gradient: 	2
image: 			header-2.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

### Port-Forwarding / Inbound NAT

Port forward `TCP 80` on WAN address `x.x.x.x` to `192.168.0.50:80`:

```
ip nat inside source static tcp 192.168.0.50 8080 x.x.x.x 80 extendable
```

### Port-Forwarding / Inbound NAT for a range of ports

Port forward `UDP 10000:20000` to `192.168.0.50`:

{% highlight bash %}
ip nat pool PORTFWD 192.168.0.50 192.168.0.50 netmask 255.255.255.0 type rotary
access-list 100 permit udp any any range 10000 20000
ip nat inside destination list 100 pool PORTFWD
{% endhighlight %}

### Revert changes

Revert running config to the startup config, without `reload`ing:

```
configure replace nvram:startup-config
```

### RTFM

[The Exim Home Page](http://www.exim.org/)
