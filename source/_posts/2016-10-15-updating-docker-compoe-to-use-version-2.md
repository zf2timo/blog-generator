---
title: Blog publishing on Github with Sculpin
tags: [docker,devOps]
categories: [development]

---

Error Message
```text
ERROR: In file './docker-compose.yml' service 'version' doesn't have any configuration options. All top level keys in your docker-compose.yml must map to a dictionary of configuration options.
```

Current Version:
```bash
$ sudo docker-compose --version
docker-compose version 1.5.2, build unknown
```

Uninstall docker:
```bash
$ sudo apt purge docker-compose
```

Needed docker-compose version: 1.8
[Download](https://github.com/docker/compose/releases)

new version: 
```bash
$ sudo docker-compose --version
docker-compose version 1.8.1, build 878cff1
```

[Install docker engine](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

```bash
$ sudo service docker start
$ sudo docker-compose up -d
```
