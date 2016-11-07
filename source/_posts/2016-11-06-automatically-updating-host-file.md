---
title: Automatically updating host file
tags: [ad-blocking,host file,automating]
categories: [security]

---

# Make the internet green again

Most internet useres theses days are using Browser Plugins like AdBlocker Plus UBlock, NoScript, Privacy Badger to protect against suspicious ads, tracking mechanismen and other things.
A downside of this technic is that the plugins have to be installed in all browser that are used &dash; additionally the settings have to be made multiple times.

An alternative way to block all the suspicious servers is to use the local host file and redirect the requests to the localhost.
But sheer amount of ad-, tracking- and other suspicious server it is a big job to keep your host file up to date.


```bash
sudo sh -c 'wget -O someonewhocares.hosts http://someonewhocares.org/hosts/hosts; cat someonewhocares.hosts /etc/hosts | grep -v -e "^[[:space:]]*$" | grep -v -e "^#" | sort | uniq > /etc/hosts; rm someonewhocares.hosts'
```


