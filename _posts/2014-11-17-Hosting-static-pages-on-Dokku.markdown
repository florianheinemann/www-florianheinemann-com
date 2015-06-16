---
layout: post
title:  "Hosting static pages on Dokku"
date:   2014-11-17 11:05:31
categories: github dokku
---

Surprisingly, Dokku (and also Heroku) [doesn’t offer](https://github.com/progrium/buildstep/blob/master/builder/config/buildpacks.txt) you a straightforward option to deploy static websites. Sure, a lot of websites are anyway dynamic nowadays, but there is still plenty of need for static pages such as blogs created by the likes of [Wintersmith](http://wintersmith.io/).

The following steps will show you how to make it anyway happen with the help of a [custom buildpack](https://github.com/florianheinemann/buildpack-nginx) that I’ve been working on. What it does is to compile and deploy a lightweight [NGINX](http://nginx.org/) instance that serves all the files.

All you have to do are the following three steps:

1. Add a file called `.env` to the root of your website directory. The file should have the following content: `export BUILDPACK_URL=https://github.com/florianheinemann/buildpack-nginx.git`

2. Add second, *empty* file called `.static` to the same directory

3. Push your project to Dokku: `git push [your server] master`

The static files that you want to host should be similarly in the root directory together with the `.env` and `.static` file. Don’t worry, those two files will not be served.

The first push will take a bit longer as the buildpack is downloading all the relevant source codes and compiling the packages, but every new push will reuse the already pre-compiled files making it a lot faster the second time round.

This buildpack has been successfully run on Digital Ocean instances of Ubuntu 14.04 and I assume that other configurations might work as well. Let me know if you successfully used the buildpack in different configurations.