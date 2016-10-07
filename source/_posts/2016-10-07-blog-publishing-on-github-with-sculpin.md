---
title: Blog publishing on Github with Sculpin
tags: [sculpin, github]
categories: [development]

---

Github offers its users a great feature, to publish a static HTML Page on its servers -  like this one you currently 
reading on. In this post i want to show you, how my setup and publishing process looks like.

## Generating the static Page
A perfect addtion to Github Sites are static Site generators. These tools converts markdown files into HTML files. 
Github promots Jekyll as site generator, but you have to hassle with Ruby, so i decieded to use [Sculpin](https://sculpin.io/) 
instead. It is written in PHP which is already installed on all of my Workstations and i am the most experienced with it.

After the installation via composer, a local server can be started, to watch the changes:
~~~bash
$ ./vendor/bin/sculpin generate --watch --server
~~~
This server can accessed via [localhost:8000](http://localhost:8000) to view the latest version of the site.
If a change was made to the layout or a post, sculpin re-generates the site automatically for you.

When its done, new repositories are needed on Github.

## Preparations and Limitations

The site will be published in a own Repository with a defined naming scheme. These have to be `$username.github.io` - 
in my case it is `zf2timo.github.io`. This name is also the domain name to browse the site.

Since i have a standard Account, the source of the Site has to be in the root of the master branch. There are 
[also options](https://help.github.com/articles/user-organization-and-project-pages/) to publish into a folder, 
but these are only for organisations available.
Because i wanted to have the generated site seperated form the sculpin configuration files for sculpin, i had to look 
for another way. The soultion was to created another repository - named `blog-generator` - 
where all the files for sculpins versioned.

## Publishing to Github.
