---
layout: post
title: "Open Source Community for Collaboration Skill Practice"
date: 2015-12-23 21:19:14 -0800
comments: true
categories: 
---


Earlier in the month, I shared some feelings about [examining tools with the devops lens](http://sysadvent.blogspot.com/2015/12/day-2-examining-tools-with-devops-lens.html). In this article, let's dig into more of the technical aspects of working with some of these tools that enable automation and give us increased understanding, transparency, and collaboration.

One of the best things about open source communities is practicing collaboration. One of the worst things, is that how to work with each project can be implicit.

In this example, I'll illustrate collaboration with tools using the [Chef community cookbook `users`](https://github.com/chef-cookbooks/users) open source project. I'm using the `users` cookbook as an example as even if someone doesn't know about the intricacies of using Chef, they can still contribute to improving this project because this specific cookbook is about managing users and groups on a system. The goal of the `users` cookbook is to distill the complexities of what is required when adding a user to a system on various platforms into an easy to use resource. This is challenging due to the differences per platform.

In community cookbooks managed by Chef, a `CONTRIBUTING.md` doc refers to a centralized [CONTRIBUTING.md doc](https://github.com/chef-cookbooks/community_cookbook_documentation/blob/master/CONTRIBUTING.MD). Including a CONTRIBUTING doc (or a reference to contributing within the README.md) is a recommended practice for open source projects. GitHub will include a banner linking to this doc to potential contributors if it exists.  This allows you to describe up-front the ways in which you would best like to interact with contributions, and the types of contributions that you would and would not like to recieve. For instance, if your project is written in Python, but you don't care for PEP-8, you could state there that a contribution of applying PEP-8 conventions would be unwelcome. 

Often these contributing documents sketch out only the minimum processes to get started but there are many workflows and branching strategies that individuals use to collaborate and resolve the conflicts that arise with different perspectives and approaches. 

Many learning git tutorials give experience with solo git, but leave out the complexities of collaborative tool use. One can read up on the intricacies of git usage, but without a way to practice, understanding git workflows can be difficult. 

## Git Configuration Files

One way to learn about some of the hidden secrets of git is to examine dotfiles available on GitHub. If something doesn't make sense review the [git documentation](https://git-scm.com/docs/git-log). Let's take a look at a modified example alias from [Fletcher Nichol's dotfile](https://github.com/fnichol/dotfiles/blob/master/home/.gitconfig).

```
graph = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset %C(cyan)(%an)%Creset' --date=relative
```

The `--graph` option creates a text based graphical representation of the commit history.

With the `--pretty` flag, you can specify a formating string.

The format string allows us to focus on what we want to see when looking at the history of commits. In this alias, the symbols translate to showing us the following information in the specific colors.

```
%h: abbreviated commit hash
%d: ref names
%s: subject
%cr: committer date, relative
%an: author name
```

Finally `--date=relative` shows dates relative to the current time, e.g. “2 hours ago”.

When using `git graph` with this alias, it gives you output like the following:

<img src="http://www.jendavis.org/assets/git_graph_example.png" alt="Example of git graph in action.">

This makes it easy to see recent commits. If there is a commit of interest, this view makes it really easy to just do `git show` of the object you want to inspect. 

Examining past commits helps us understand how the code is structured on a project, as well as some of the design patterns that project uses for git workflows.

## Issues and Pull Requests
Looking at open [issues](https://github.com/chef-cookbooks/users/issues) and [pull requests](https://github.com/chef-cookbooks/users/pulls) ("PR") we can obtain additional information about the project and get an idea of the needs of consumers.

[Travis](https://docs.travis-ci.com/user/for-beginners) is a hosted, distributed and continuous integration service used to build and test projects. [Travis integration](https://travis-ci.org/) is free for open source projects. This provides one mechanism for testing pull requests prior to integration to give some level of confidence about risk. The [.travis.yml](https://github.com/chef-cookbooks/users/blob/master/.travis.yml) file defines the configuration. 

We can look at a sample pull request (PR), [Pull Request 117](https://github.com/chef-cookbooks/users/pull/117) from [Arnoud Vermeer](https://github.com/funzoneq). The GitHub GUI will link to a [build](https://travis-ci.org/chef-cookbooks/users/builds/85706180). We can see that [Pull Request 117](https://github.com/chef-cookbooks/users/pull/117) has a failure with the `rubocop` check.

<img src="http://www.jendavis.org/assets/example_pr117_failure.png" alt="Pull Request 117 rubocop failure.">

When we look at a PR we may find that there are changes we want to accept and changes that we don't want to accept. We can cherry pick explicitly what we want to accept with the `cherry-pick` command with git, or we can adopt different work flows that have a similar effect. 

### Examining a Pull Request - Example 1 
To facilitate working with [Pull Request 117](https://github.com/chef-cookbooks/users/pull/117), let's incorporate another helpful git [alias](https://github.com/fnichol/dotfiles/blob/master/home/.gitconfig), `git pr`:

```
pr = "!_git_pr() { git fetch origin pull/$1/head:pr-$1 && git checkout pr-$1; }; _git_pr"
```

This allows us to quickly pull down and examine someone's contributions from a PR. In this case, I want to pull down PR 117 in the `users` cookbook and examine it. 


```
➜  users git:(master) git pr 117
remote: Counting objects: 8, done.
remote: Total 8 (delta 4), reused 4 (delta 4), pack-reused 4
Unpacking objects: 100% (8/8), done.
From github.com:chef-cookbooks/users
 * [new ref]         refs/pull/117/head -> pr-117
Switched to branch 'pr-117'
```

We can examine the commits in the pull request with `git graph`.

<img src="http://www.jendavis.org/assets/git_graph_users_before.png" alt="Output of git graph with alias">

This shows two commits `7623e00` and `bc74a45`. 

The main changes are in `bc74a45`. In this commit the contributor is adding code, so that on FreeBSD platforms it checks to see if the shell specified in the databag json object exists on the node as specified, or in /usr/local. If the shell isn't available in these two locations, we set the shell to the FreeBSD default shell `/bin/sh`. This PR exposes some fragility in our current definition as we don't check the existence of the shell on any other platform. Depending on our current priority and workload we may rewrite the resource to be less fragile or accept the contributions as they are. 

### Examining a Pull Request - Example 2 

There are additional utilities that can help us beyond just the simple git aliases that we can construct. One example is [hub](https://hub.github.com/). As a wrapper around git, [hub](https://hub.github.com/) provides some useful additions to the git client making it easier to work with PRs. Once you've [installed](https://hub.github.com/) hub, you can see the project's issues, open up a project's wiki, and a number of other options from the command line. 

When working with a PR, you can quickly create a new branch with its contents with a simple checkout:

```
git checkout https://github.com/chef-cookbooks/users/pull/117
```

Similar to the `pr` alias:

```
➜  users git:(master) git checkout https://github.com/chef-cookbooks/users/pull/117
Updating funzoneq
remote: Counting objects: 8, done.
remote: Total 8 (delta 4), reused 4 (delta 4), pack-reused 4
Unpacking objects: 100% (8/8), done.
From git://github.com/funzoneq/users
 * [new branch]      master     -> funzoneq/master
Branch funzoneq-master set up to track remote branch master from funzoneq.
```

This will create an appropriate named branch, and allow you to take what you want from the PR and add any necessary changes. For example if a PR has minor failures with any test cases, you might want to checkout the PR, tweak it until any failing test passes, and then commit the code.

After checking out the PR, the commits can be evaluated.

####  Squashing Commits
```
git rebase origin/master -i
```

Commits can be skipped, squashed, or edited interactively. Squashing is the process of taking one or more commits and merging it into a previous commit. This is useful to simplify the set of commits that a peer has to review. For just this reason, some projects prefer that commits be rebased or squashed prior to sending a pull request. Some organizations or teams discourage the practice of rebasing or squashing in order to have a high amount of verbosity and code history. Check the contributing documentation or talk to a team member before you adopt a specific practice.

```
pick bc74a45 Check if shell exists on FreeBSD. If not, fall back to /bin/sh by default. If it's a manually installed shell, then it lives in /usr/local/bin/{bash,zsh,rbash}
pick 7623e00 Make Travis CI happy

# Rebase 72d3800..7623e00 onto 72d3800
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```
I can modify the second `pick` to `s` and squash this into a single commit.

When I squash the commit, it creates a new object. After I squash the commit, `git graph` shows me a new commit object.

<img src="http://www.jendavis.org/assets/git_graph_users_after.png" alt="Output of git graph after commit squashed.">

#### Testing 
I can now test to see if the travis issue is still a problem in the current branch by running `rubocop`, the command that was failing in the Travis Build earlier manually.

```
  users git:(funzoneq-master) rubocop
Inspecting 16 files
................
```
With rubocop, a `.` represents a file without issues. 

```
git push -fu origin funzoneq-master
```

This sets up a tracking branch and force pushes the edit of the history. In this example, it gives me the option to do a PR (which I did), resulting in [Pull Request 123](https://github.com/chef-cookbooks/users/pull/123). This is possible because I have permission to commit to this repository. 

### Examining an Issue 

Let's take a look at a reported issue, [Issue 118](https://github.com/chef-cookbooks/users/issues/118). In this issue, [Chris Gianelloni](https://twitter.com/wolf31o2) reported a problem with the `users` cookbook on Mac OS X.

There is no PR in this case, so I create a branch with `git checkout -b`

```
git checkout -b issues_118
```

In the earlier example, I skipped over how to validate that the code actually worked on the system. We can manually test the code if we had a Mac OS X laptop using the [`chef-apply` command](https://docs.chef.io/ctl_chef_apply.html), an executable that runs a single recipe from the command line.  

Examining the cookbook structure shows that there are [chefspec tests](https://github.com/chef-cookbooks/users/tree/master/spec), but no other tests. Inside the `test` directory, there is only a fixtures directory that includes sample cookbooks. This exposes the risk of making changes to code in this project. 

In last years sysadvent, I introduced writing [custom resources](https://docs.chef.io/custom_resources.html) and using [Test Kitchen](http://kitchen.ci/) in the [Baking Delicious Resources with Chef article](https://www.chef.io/blog/2014/12/22/sysadvent-day-21-baking-delicious-resources-with-chef/). [Test Kitchen](http://kitchen.ci/) is an implementation of sandbox automation that can run on a individual's computer and integrates with a number of different cloud providers and virtualization technologies including Amazon EC2, CloudStack, Digital Ocean, Rackspace, OpenStack, Vagrant, and Docker. It has a static configuration that can be easily checked into version control along with a software project.

#### Using Test Kitchen to Spin Up Instances

Inside the `users` cookbook, there is a [`.kitchen.yml`](https://github.com/chef-cookbooks/users/blob/master/.kitchen.yml) that has a vagrant driver and the chef_zero driver with a number of platforms. This would allow us to test any of the platforms listed with vagrant and virtualbox.

Apple's EULA has implications towards Mac OS X image availability. While there are some images available on the internet, organizations (and individuals) have to define how to meet Apple's legal requirements. Within Chef, we use [Atlas](https://atlas.hashicorp.com/) to store private images for employees use.

To test Mac OS X, I created a new file `.kitchen.vmware.yml` with the following configuration:

```
driver:
  name: vagrant
  provider: vmware_fusion
  customize:
    numvcpus: 2
    memsize: 2048

provisioner:
  name: chef_zero

platforms:
  - name: macosx-10.11
    driver:
      box: chef/macosx-10.11 # private
```
Once I do a `vagrant login` on the command line I can now download the image. I created a symlink to `.kitchen.vmware.yml`

```
ln -s .kitchen.vmware.yml .kitchen.local.yml
```
*Note* It's also possible to just define environment variable `KITCHEN_LOCAL_YAML` rather than creating a symlink.

I can list my instances and see the Mac OS X 10.11 images.

```
➜  users git:(issues_118) ✗ kitchen list
Instance               Driver   Provisioner  Verifier  Transport  Last Action
default-macosx-1011    Vagrant  ChefZero     Busser    Ssh        <Not Created>
sysadmins-macosx-1011  Vagrant  ChefZero     Busser    Ssh        <Not Created>
```

I converged `kitchen converge default-macosx-1011`  and reproduced the issue that [Chris](https://twitter.com/wolf31o2) reported. 

```
================================================================================
           Error executing action `create` on resource 'user[test_user]'


           ArgumentError
           -------------
           can't find user for test_user

```

Logging into the host with `kitchen login default-macosx-1011`, I could check to see if the user was created with the `dscl` command.

```
 vagrant$ dscl . list /Users | grep test_user
test_user
```

After digging a little further, and some pair code review with [Nathen Harvey](https://twitter.com/nathenharvey) we discovered that the issue was with the directory resource wanting a UID rather than a username when declaring the owner on Mac OS X.

Switching from username to UID resolved the errors, but this only tested against Mac OS X. We should do some tests against other operating systems to make sure we haven't broken the provider. 

To speed up tests, I use Docker rather than trying to spin up that many VMs with Virtual Box or VMWare. I already have docker-machine installed, if you don't check out this [getting started guide](https://docs.docker.com/machine/get-started/).

```
➜  users git:(issues_118) ✗ docker-machine start  default
Started machines may have new IP addresses. You may need to re-run the `docker-machine env` command.
➜  users git:(issues_118) ✗ docker-machine env default
➜  users git:(issues_118) ✗ eval "$(docker-machine env default)"
```

I'm going to use [someara's](https://twitter.com/someara) [kitchen-dokken](https://github.com/someara/kitchen-dokken) plugin rather than kitchen-docker. After cleaning up my previous run with `kitchen destroy`, I update the symlink to point to `.kitchen.dokken.yml`. Now when I issue a `kitchen list`:

```
➜  users git:(issues_118) ✗ kitchen list
Instance               Driver  Provisioner  Verifier  Transport  Last Action
default-centos-6       Dokken  Dokken       Busser    Dokken     <Not Created>
default-centos-7       Dokken  Dokken       Busser    Dokken     <Not Created>
default-fedora-21      Dokken  Dokken       Busser    Dokken     <Not Created>
default-debian-7       Dokken  Dokken       Busser    Dokken     <Not Created>
default-ubuntu-1204    Dokken  Dokken       Busser    Dokken     <Not Created>
default-ubuntu-1404    Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-centos-6     Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-centos-7     Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-fedora-21    Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-debian-7     Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-ubuntu-1204  Dokken  Dokken       Busser    Dokken     <Not Created>
sysadmins-ubuntu-1404  Dokken  Dokken       Busser    Dokken     <Not Created>
```

A successful `kitchen create` and `kitchen converge -c` confirm that the changes work as expected. `kitchen converge -c` will run a converge against all matching instances concurrently.

Since there are no integration tests, we manually login in and check whether the home directory gets created as expected.

```
root@079f902cf103:/home/test_user# ls -al
total 24
drwxr-xr-x 3 test_user test_user 4096 Dec 20 07:02 .
drwxr-xr-x 3 root      root      4096 Dec 20 07:02 ..
-rw-r--r-- 1 test_user test_user  220 Apr  9  2014 .bash_logout
-rw-r--r-- 1 test_user test_user 3637 Apr  9  2014 .bashrc
-rw-r--r-- 1 test_user test_user  675 Apr  9  2014 .profile
drwx------ 2 test_user root      4096 Dec 20 07:02 .ssh
```

After manual verification, I commited and checked in the code, and created a [PR](https://github.com/chef-cookbooks/users/pull/124).

## More Than Code

The writing process I follow with sysadvent uses some of these collaborative tips. I post my article up on GitHub in a private repository, and then invite my peer reviewers to the repository. 

While collaboratively writing [Effective Devops](http://shop.oreilly.com/product/0636920039846.do) with [Katherine Daniels](https://twitter.com/beerops), we used git, AsciiDoc, and O'Reilly's Atlas; a git-backed web-based platform for publishing books. 

The lightweight formats of markdown and AsciiDoc can be collaborative with the use of git. I find limitations compared to more traditional writing tools are around GUI formating within the editors I use. I regularly find myself having to do a little extra commits to the repository to check what the browser view or generated PDF looks like with included images. Overall, this is a small price to pay when getting the benefit of a stronger piece through collaboration. Some of these limitations may be overcome with the use of extensions available in specific editors.

## Summary

Using [Test Kitchen](http://kitchen.ci/) allows me to quickly change which set of tools I want to use - docker, vagrant with Virtual Box, or vagrant with VMWare - depending on the current need. The kitchen configuration files can be saved alongside the project allowing anyone to quickly get going and collaborate from a consistent point.

Combined with the flexibility of [Test Kitchen](http://kitchen.ci/), Vagrant allows us to combine private and publicly available resources so if you are in a situation where you are working on something internal to your company while also contributing to Open Source, you can manage that complexity. In the above example, I'm providing my team with knowledge of how to replicate my testing without adding initial complexity to the base `.kitchen.yml`. It allows me to be transparent about my process without blocking people who don't have access to Chef's internal images or VMWare Fusion.

Additionally, local git configurations or tools like [hub](https://hub.github.com/) can simplify the collaboration process allowing us to cherry pick our commits. Talk to your team, peers in the industry, or review a project's CONTRIBUTING.md file to discover other mechanisms that individuals use when working.

Here are a few examples of helpful git snippets that other folks shared with me via Twitter:

<blockquote class="twitter-tweet" data-conversation="none" lang="en"><p lang="und" dir="ltr"><a href="https://twitter.com/sigje">@sigje</a> <a href="https://t.co/CR2HURUcmk">https://t.co/CR2HURUcmk</a></p>&mdash; Robb Kidd (@robbkidd) <a href="https://twitter.com/robbkidd/status/678225258994905088">December 19, 2015</a></blockquote>

<blockquote class="twitter-tweet" data-conversation="none" lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/sigje">@sigje</a> My favorite git alias:&#10;&#10;up = &quot;!f() { git stash &amp;&amp; git pull --rebase origin master &amp;&amp; git stash pop; }; f&quot;</p>&mdash; Joe Nuspl (@JoeNuspl) <a href="https://twitter.com/JoeNuspl/status/678480616724152320">December 20, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Kennon Kwok also shared [tig](https://github.com/jonas/tig), a text mode interface for Git as a useful utility.

In addition, folks mentioned [Seth Vargo](https://twitter.com/sethvargo) as being the inspiration for some common habits, and Seth has kindly shared his [Git config](https://gist.github.com/sethvargo/73dd1d915411ebffaec0).

## Further Resources

* [Emma Jane Hogbin Westby's Git for Teams](http://gitforteams.com/)
* [Atlassian git rebase history](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase-i)
* [Travis CI for Complete Beginners](https://docs.travis-ci.com/user/for-beginners)
* [Continuous Integration article from Martin Fowler](http://www.martinfowler.com/articles/continuousIntegration.html)
​* [Introduction to Rubocop with Frank Webber](https://www.youtube.com/watch?v=HRrc6UCXFMs)
* [Test your Infrastructure Code - Chef Skill Library](https://learn.chef.io/test-your-infrastructure-code/rhel/)
* [Atlas documentation](https://atlas.hashicorp.com/help)
* [Docker Machine](https://docs.docker.com/machine/) and [Getting Started](https://docs.docker.com/machine/get-started/)
* [kitchen-dokken](https://github.com/someara/kitchen-dokken)

## Thank you!

Thank you [H. Waldo Grunenwald](https://twitter.com/gwaldo), [Robb Kidd](https://twitter.com/robbkidd), [Carlos Maldonado](https://twitter.com/kamihack), [VM Brasseur](https://twitter.com/vmbrasseur), and [Kennon Kwok](https://twitter.com/kennonkwok) for peer review and aditional edits. 

Thank you to all of the [Chef Community Engineering Team](https://twitter.com/chef) that provided answers to my questions over the last few months inspiring this article. 

Thank you to [Arnoud Vermeer](https://github.com/funzoneq) for contributing [PR 117](https://github.com/chef-cookbooks/users/pull/117) and [Chris Gianelloni](https://twitter.com/wolf31o2) for contributing [Issue 118](https://github.com/chef-cookbooks/users/issues/118) giving me the opportunity to add context to talking about collaboration with reported issues and pull requests. Your continued contributions to the Chef community are valued and appreciated!