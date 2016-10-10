---
title: Blog publishing on Github with Sculpin
tags: [sculpin, github]
categories: [development]

---

Github offers its users a great feature, to publish a static HTML Page on its servers -  like this one you currently 
reading on. In this post i want to show you, how my setup and publishing process looks like.

## Generating the static Page
A perfect addition to Github Sites are static Site generators. These tools converts markdown files into HTML files. 
Github promotes Jekyll as site generator, but you have to hassle with Ruby, so i decided to use [Sculpin](https://sculpin.io/) 
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
in my case it is [`zf2timo.github.io`](zf2timo.github.io). This name is also the domain name to browse the blog.

Since i have a standard Account, the source of the Site has to be in the root of the master branch. There are 
[also options](https://help.github.com/articles/user-organization-and-project-pages/) to publish into a folder, 
but these are only for organisations available.
Because i wanted to have the generated site separated form the configuration files for sculpin, i had to look 
for another way. 
The solution was to created another repository - named [`blog-generator`](https://github.com/zf2timo/blog-generator) - 
where all the files for sculpins versioned.

Time to combine these two repositories.

## Publishing to Github

My process to publish the blog contains theses steps:

- switch to the repository `blog-generator`
- clone the `zf2timo.github.io` repository in a sub-folder, when its not exists
- generate the new html files with `sculpin`
- copy them into the `zf2timo.github.io` folder
- switch in the sub-folder of `zf2timo.github.io`
- commit and push all changes to Github

In the moment of the push, the updated is published (i'am sure, there are running some task in the background on Github,
but i didn't noticed a delay yet)

Because this are always the sames steps, i created the [`publish.sh`](https://github.com/zf2timo/blog-generator/blob/b0aaf4f08963f42aabe24fde3b4e1952fb7e5d79/publish.sh) 
file, that do all this steps for me and i just have to execute it.


