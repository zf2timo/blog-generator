---
title: Empty server name in XDEBUG
tags: [docker, xdebug]
categories: [development]
---
#Empty server name in XDEBUG

Today I build a new docker environment for a project with a really simple setup. All I needed
was a php and nginx container. 
I had both created for other projects several times without big issues.
But as I started to debug the application, PHPStorm wasn't able to map the remote directory to a local directory.
For the first debug session this is normal and you have to configure this manually.

But this time I had another message in my debug window:

![PHPStorm debug window with error](/images/posts/2017-12-14-debug-error-window.png "PHPStorm Debug window")

While checking my PHPStorm configuration I noticed a Server without a name in the "Run\Debug configurations > Servers" window.
I did not created a config like this one. 

After some research on the internet I finally found the solution:
My NGINX did not send a Server name in the response. For this reason my IDE was not able to create a proper configuration and 
map the local directories to remote directories.
 
To Fix the problem only a single line was missing in my `/etc//nginx/sites-available/default.conf`

```nginx
fastcgi_param SERVER_NAME $server_name;
```

With this configuration the debugging works smooth as usually.

