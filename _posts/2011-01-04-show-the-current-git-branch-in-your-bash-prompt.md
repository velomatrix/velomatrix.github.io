---
layout: post
title:  "Show the current git branch in your bash prompt"
date:   2011-01-04 02:05:00 -0600
permalink: /2011/01/04/show-the-current-git-branch-in-your-bash-prompt
author: ryin
categories:
- tools
tags:
- bash
- branching
- git
---
[git](http://git-scm.com/) is the current hotness in source control. One of its main strengths is cheap and easy branching and merging. As a result, git users tend to use branches often. This is a good thing. However, when working on multiple repositories with multiple branches, it can be easy to lose track of your current branch.

While a simple ``git status`` will yield the current branch, it is often convenient to have the current branch displayed in your prompt. The magical incantation to add to your ``PS1`` variable is ``$(__git_ps1)``. This function is defined in ``/etc/bash_completion.d/git``. If you don’t have access to that file, you can find it in ``contrib/completion/git-completion.bash`` after cloning this repo:

    git://git.kernel.org/pub/scm/git/git.git

Here is a snippet from a .bashrc file for displaying the current git branch in your bash prompt:

    source /etc/bash_completion.d/git
    export PS1='\w$(__git_ps1 "(%s)") > '

