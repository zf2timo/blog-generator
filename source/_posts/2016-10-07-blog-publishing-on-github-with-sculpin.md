---
title: Blog publishing on Github with Sculpin
tags: [sculpin, github]
categories: [development]

---

Github offers its users a great feature, to publish a static HTML Page on its servers -  like this one you currently 
reading on. In this post i want to talk about, how my process looks like.

## Generating the static Page
A perfect addtion to this feature are static Site generators. These tools converts markdown files into HTML files. 
Github promots Jekyll as site generator, but you have to hassle with Ruby, so i decieded to use [Sculpin](https://sculpin.io/) 
instead. It is written in PHP which is already installed on all of my Systems and i am the most experienced with it.

After the installation via composer, a local server can be started, to watch the changes:
~~~bash
$ ./vendor/bin/sculpin generate --watch --server
~~~
This server can accessed via [localhost:8000](http://localhost:8000) to view the latest version of the site.
If a change was made to the layout or a post, sculpin re-generates the site automatically for you.

## Preparations and Limitations

The site will be published in a own Repository wiht a defined naming schame. These have to be `$username.github.io` - 
in my case it is `zf2timo.github.io`. This name is also the domain name to browse the site.

My Account is a normal Account, so i have to publish the page in the root of my repository. There are also options to 
publish into a folder, but these are only for organisations available.
Because i wanted to have the generated site seperated form the sculpin configuration files for sculpin, i had to look 
for another way. The soultion was to created another repository - named `blog-generator` - 
where all the files for sculpins versioned.

## Publishing to Github.
