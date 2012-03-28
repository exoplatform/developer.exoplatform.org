---
layout: page
title: "Git - Startup Guide"
tags: [git]
group: git
---
{% include JB/setup %}

Early in April 2012, eXo moved its projects from [Subversion](https://svn.exoplatform.org) to [Git](http://git-scm.com/).
Our Git repositories will be hosted on [GitHub](https://www.github.com/exoplatform/).

This guide doesn't target to learn you everything about Git but just to give you the necessary skills and pointers to start.

# GitHub

GitHub is the platform we chose to host our Git repositories.
**To contribute to eXo projects you have to create a [GitHub](https://www.github.com/) account.**

For eXo employees it is recommended to create one with the same username as the one provided by the company (GoogleApp Id) when you joined us.
**You have to commit using your exoplatform.com email by setting it in your global git configuration or locally into each eXo repository clone** (see below).

TODO : Info about rights management

GitHub provides a lot of [documentation](http://help.github.com/) and especially an installation/configuration guide for each operating system :

* [Linux](http://help.github.com/linux-set-up-git/)
* [Windows](http://help.github.com/win-set-up-git/)
* [MacOS](http://help.github.com/mac-set-up-git/)

Please follow these guides to setup your environment.

# Git & IDE

Git is natively supported by all IDE :

* Eclipse : [EGit plugin](http://www.eclipse.org/egit/) bundled by default in the major part of eclipse distributions.
* IntelliJ : [Native](http://www.jetbrains.com/idea/webhelp/using-git-integration.html)
* Netbeans : [Native since 7.1](http://netbeans.org/projects/versioncontrol/pages/Git_main)

# Git Configuration

It is recommended to create an SSH private key (with a password) and to use it to access to your Git(Hub) repositories (see Github guides above).

By default you have at least to setup your default identity that will be used for all git instances on the system if you don't override them locally.

{% highlight sh %}
$ git config --global user.name "John Doe"
$ git config --global user.email "jdoe@exoplatform.com"
{% endhighlight %}

We recommend also :

* to configure git to activate use colors if you terminal supports it :

{% highlight sh %}
$ git config color.ui true
{% endhighlight %}

* to configure git to push only the current branch by default to avoid to send to the server some changes in others branches you weren't ready to share

{% highlight sh %}
$ git config --global push.default current
{% endhighlight %}

* to configure git to add some command aliases to easily call them with `git <ALIAS_NAME>`.
You just add a section `[alias]`in your `~/.gitconfig` file with entries like bellow

{% highlight ini %}
[alias]

	##### Basic aliases
	# Long status
	st = status
	# Short status
	s = status -s
	# Show all branches
	br = branch -a
	# Show branches with commit message
	sb = show-branch
	# Commit
	ci = commit
	# Checkout
	co = checkout
    # Show remote repositories
	r  = remote -v
    # Amend last commit
    amend = ci --amend
	# Removes files/directories from staging
	unadd = rm -r --cached

    ##### Diff aliases
	# Diff and show commands with word-diff style
	wd = diff --word-diff
	ws = show --word-diff
	# Show diff before pull
	do = diff ORIG_HEAD HEAD
	# Show modified lines in the index
	staged = diff --cached
	# Show modified files
    changes= diff --name-status -r
	# Diff with statistics
    ds = diff --stat -r

    ##### Log aliases
    # Show HEAD commit
	head = log --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative -n1
	# Short one line logs with ref-names
	l  = log --oneline --decorate=short
	# Shows the last git logentry (hash, author, date commitmessage)
	llm = log -1
	# Short one line logs with ref-names and statistics
	gl = log --oneline --decorate --stat --graph
    # Short one line logs with ref-names (yellow, date (green) and author (blue)
	glog = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
	# Show last commit
	lc = log ORIG_HEAD.. --stat --no-merges
	# Graph log with full commit message
	glaaa = log --graph --abbrev-commit --date=relative

    ##### Misc
	# Show last commiter
	whois = !sh -c 'git log -i -1 --pretty=\"format:%an <%ae>\n\" --author=\"$1\"' -
	# Show last commit message
    whatis = show -s --pretty='tformat:%h (%s, %ad)' --date=short
	# Hash of HEAD
	h = rev-list --max-count=1 HEAD
	# Show users which have commits in current branch
	ul = !git log --format='%aN' | sort -u
	# Number of commits in current branch
	c  = !git log --oneline | wc -l
	# Creates a tar.gz archive named after the last commits hash from HEAD! in the directory above the repository
	ahg = !git archive HEAD --format=tar | gzip > ../`git h`.tar.gz
	# shows ignored directories
	ignored = !git ls-files --others -i --exclude-standard --directory
    # Move to the root of the repository
	root = !cd $(git rev-parse --show-cdup)
	# Show the root directory of the repository
	sroot = rev-parse --show-toplevel
	# Prune remote branches
	prune-all = !git remote | xargs -n 1 git remote prune
	# Show aliases
	aliases = !git config --get-regexp 'alias.*' | colrm 1 6 | sed 's/[ ]/ = /'
	# Show upstream for the current branch
    upstream = !git for-each-ref --format='%(upstream:short)' `git symbolic-ref HEAD`
{% endhighlight %}
