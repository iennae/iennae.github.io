---
layout: post
title: "Octopress Tips to Myself"
date: 2015-01-04 00:20:00 -0800
comments: true
categories: blogging
published: true

---

When building from source to add new posts.

{% codeblock lang:bash %}
$ git clone git@github.com:REPO
$ cd REPO
$ git checkout -b source origin/source
$ mkdir _deploy
$ rake new_post["TITLE"]
{% endcodeblock %}

Write blog entry.  

{% codeblock lang:bash %}
$ rake generate
$ rake deploy
$ git add .
$ git commit -m 'MESSAGE'
$ git push origin source
{% endcodeblock %}

For zsh issues for [rake new_post](https://github.com/imathis/octopress/issues/117).