---
title: Blog publishing on Github with Sculpin
tags: [sculpin, github]
categories: [development]

---

There is a great feature on Github to easily publish a static HTML Page on its servers - like this one you are currently 
reading on. Read through my documentation to find out what my setup and publishing process looks like.

## Generating the static Page
A perfect addition to Github Sites are static Site generators. These tools convert markdown files into HTML files. 
Github promotes Jekyll as a site generator, but you have to hassle with Ruby, therefore I decided to use [Sculpin](https://sculpin.io/),
which is written in PHP that is already installed on all of my Workstations. And I am the most experienced with PHP.

After the installation via composer a local server can be started to watch the changes:
~~~bash
$ ./vendor/bin/sculpin generate --watch --server
~~~
This server can be accessed via [localhost:8000](http://localhost:8000) to view the latest version of the site.
If a change is made in the layout or a post, sculpin re-generates the site automatically for you.

When it's done, new repositories are needed on Github.

## Preparations and Limitations
The site will be published in an own Repository with a defined naming scheme. These have to be `$username.github.io` - 
in my case it's [`zf2timo.github.io`](zf2timo.github.io). This name is also the domain name to browse through the blog.

Since I have a simple user Account, the source of the Site has to be in the root of the master branch. There are 
[also options](https://help.github.com/articles/user-organization-and-project-pages/) to publish into a sub-folder, 
but these are only available for organisations.
But as I wanted to have the generated site separated from the configuration files for sculpin, too, I had to look 
for another way. 
I found the solution in creating another repository - named [`blog-generator`](https://github.com/zf2timo/blog-generator) - 
where all the files for sculpins are versioned.

Now it's time to combine these two repositories.

## Publishing to Github
My process to publish the blog involves the following steps:

- switching to the repository `blog-generator`
- cloning the `zf2timo.github.io` repository in a sub-folder, when its not exists
- generating the new html files with `sculpin`
- copying them into the `zf2timo.github.io` folder
- switching in the sub-folder of `zf2timo.github.io`
- committing and pushing all changes to Github

In the moment of pushing, the updated version is published (I am sure, there are running some tasks in the background 
on Github, but I didn't noticed a delay yet).

Because this are always the sames steps, I created the [`publish.sh`](https://github.com/zf2timo/blog-generator/blob/b0aaf4f08963f42aabe24fde3b4e1952fb7e5d79/publish.sh) 
file, that do all this steps for me and I just have to execute it.


