---
title: Automatically updating host file
tags: [ad-blocking,host file,automating]
categories: [security]

---

# Make the internet green again

These days most of the internet users use Browser Plugins to block supsicious ad and/or prevent tracking mechanism or similar from working. The most popular plugins are AdBlocker Plus UBlock, NoScript, Privacy Badger - just to name a few. A bit disadvantageous of using your plugin of choice is the mandatory installation in every browser that is used - and therefor additionally settings have to be made several times. Can be a bit stressfull when you ask me.

An alternative way to block suspicious servers is to make use of local host files and redirect the requests to the localhost. But with the huge amount of ad-, tracking- and other mistrustful servers out there it would take a lot of time and effort to to keep the `host` file up to date.

Thankfully [Dan Pollock](http://someonewhocares.org) has done this or rather is still updating the list of mistrustful servers multiple times a week. And thankfully he allows everyone to use this file.

With a few commands on Linux operating system this process of updating can be automated:
```bash
wget -O someonewhocares.hosts http://someonewhocares.org/hosts/hosts; cat someonewhocares.hosts /etc/hosts | grep -v -e "^[[:space:]]*$" | grep -v -e "^#" | sort | uniq > /etc/hosts; rm someonewhocares.hosts
```
This is a really long command, which we don't like to enter every time a new version of the list is published. Therefore let us automate the process with a cronjob:
```bash
52,22 */4 * * * wget -O someonewhocares.hosts http://someonewhocares.org/hosts/hosts; cat someonewhocares.hosts /etc/hosts | grep -v -e "^[[:space:]]*$" | grep -v -e "^#" | sort | uniq > /etc/hosts; rm someonewhocares.hosts >> /var/log/cron-host-file-update.log 2>&1
```
Please note that this cronjob has to be registered for the root user. Other users can not write to the `host` file by default.
Also the time schedule should match you're usage behaviour. 

I think, this is a easy solution to block odd server.