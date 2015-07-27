---
layout: post
title: "Working with Gists within Sublime"
date: 2015-07-26 23:47:28 -0700
comments: true
categories: 
---

[Sublime](http://www.sublimetext.com/) is a pretty sweet editor in combination with the Sublime [package manager](https://packagecontrol.io/). Today, I learned about the [Gist package add-on](https://github.com/condemil/Gist). Gists are a way to share work. Every gist is a git repository which means that it can be forked and cloned in the same ways. Gists can be public or secret. Public gists are searchable; secret gists are not, but they are accessible by anyone with the URL. Most of the time, I use gists for training classes to assign IPs, as well as snippets of code.

After installing the package, to interact with Github's gist repository generate a [new token on Github](https://github.com/condemil/Gist#generating-access-token). You can also configure the settings to use Enterprise Git. 

All of the commands to interact with Gist require 2 key combinations by default. With the [Gist package add-on](https://github.com/condemil/Gist) on OS X, Command + K is the first key combination. The second is dependent on the desired action. Command + K followed with Command + O will open up a list of available gists. Double clicking opens up a new window in sublime with the content.

To save the gist, it's more than just saving the file in Sublime, it requires the key combo of Command + K Command + S. 

