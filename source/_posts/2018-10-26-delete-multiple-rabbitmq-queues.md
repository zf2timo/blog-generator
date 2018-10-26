---
title: Delete multiple RabbitMQ Queues
tags: [rabbitmq, bash]
categories: [development]
---
#Delete multiple RabbitMQ Queues

RabbitMQ is a great tool to handle a lot of data and process them asynchronously. At my work, we have some programs, that
create dynamically the queues. 
But sometimes these queues where not processed - because of an error when testing some changes locally. In this cases you
have to remove the queues in another way.

Thankfully RabbitMQ provides a useful console tool. This can be use to create a list of queues. With some additional bash
magic all the queues can be delete in one go:
```bash
$ rabbitmqadmin -f tsv -q list queues name > q.txt
$ while read -r name; do rabbitmqadmin -q delete queue name="${name}"; done < q.txt
```
This is only a minimal snipped. It can be extended with a `grep` to run an additional filter on the queue names. Or
pass the `-V` parameter to `rabbitmqadmin` to limit everything to a specified vhost.
There is a lot more to explore. 
