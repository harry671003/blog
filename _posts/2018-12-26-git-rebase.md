---
title: "Git Rebase"
date: 2017-10-20 08:26:28 -0400
categories: git
---

I've been using git for over 5 years now. Like most programmers, I was able to survive with the very basic understanding of git. Recently, I stumbled upon the `rebase` command which would let you keep a clean and linear history.

## Rebase in a nutshell

> Rebasing is a common way to integrate upstream changes into your local repository. Without rebase you'd be resorting to a merge from master which can create ugly and unnecessary commits.

The idea behind git rebase is just simple. You have a feature branch checkout out in your local repository on which you've made some commits. While on the master branch, more commits were made after you'd created the feature branch. The command `git rebase master` lets you bring in those commits from the master branch to your feature brach.

## Visual representation
<br/>
![Git Rebase](/blog/assets/posts/2018-12-26-git-rebase/git-rebase.svg)

In the above diagram, the branch `feature` was created from commit `C` on `master`. Commits `G`, `H` and `I` were made on the `feature` branch. Meanwhile other people have pushed more changes (commits `D`, `E` and `F`) on the master branch. Rebase is the best way to bring in these commits from `master` to `feature` without messing around with a merge.

> From the above diagram: <br/>
> `master: A -> B -> C -> D -> E -> F` <br/>
> `feature: A -> B -> C -> G -> H -> I`

The command `git rebase master` would first change the base commit of the branch `feature`.

> This would result in the following:<br/>
> `feature: A -> B -> C -> D -> E -> F`

After this is done, git would then replay the commits made on feature branch one by one.

> The result would like like: <br/>
> `feature: A -> B -> C -> D -> E -> F -> G' -> H' -> I'`

*Note that the commit ID's would be different.*

## Interactive mode
Then there is the interactive mode, which would let you do things like:
- squash commits together
- split a commit

## Words of warning!
Just like popular fiction has taught us that changing history is really dangerous (Dr. Who, Butterfly Effect etc).

### Rebase often
You might get lots of merge conflicts if the branch you're rebasing has strayed away from master for too long. Rebasing often would solve this.

### Never rewrite public history
Let me say that again: Never rewrite public history.

If you rebase a public branch and later push it out with a `--force` flag, it would result in your co-workers losing their commits when they pull your commit.