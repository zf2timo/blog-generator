---
title: Automatically updating host file
tags: [ad-blocking,host file,automating]
categories: [security]

---

# Make the internet green again

Most internet user's theses days are using Browser Plugins like AdBlocker Plus UBlock, NoScript, Privacy Badger to 
protect against suspicious ads, tracking mechanism and other things. A downside of this method is that the plugins have 
to be installed in all browser that are used &dash; additionally the settings have to be made multiple times.

An alternative way to block all the suspicious servers is to use the local host file and redirect the requests to the 
localhost. But sheer amount of ad-, tracking- and other suspicious server it is a big job to keep your host file up 
to date.

Thankfully this job is done by [Dan Pollock](http://someonewhocares.org) and he allows everyone to use his file. Because
the list is updated multiple times a week it's hard to keep the host file up to date.

But with a few commands on a Linux System, this process can be automated: 
```bash
sudo sh -c 'wget -O someonewhocares.hosts http://someonewhocares.org/hosts/hosts; cat someonewhocares.hosts /etc/hosts | grep -v -e "^[[:space:]]*$" | grep -v -e "^#" | sort | uniq > /etc/hosts; rm someonewhocares.hosts'
```
As you can see I use a `sudo` command here. I have to use it, because for security reasons the host file can only be 
changed by an user with root access.
This prevents an complete automation of the process with a cronjob or start up script.
But it can be done a little bit more convenient by aliasing:
```bash
alias update-host-file='....'
```
From now on, you just have occasionally enter `update-host-file` in you're terminal and your `host` file will be updated.

I think it is a easy solution to block odd server.