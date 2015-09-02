---
layout: page
title: Version Control with Git
subtitle: Collaborating
minutes: 25
---
> ## Learning Objectives {.objectives}
>
> *  Collaborate pushing to a common repository.

For the next step, we are going to simulate collaborating. You can think of this either as collaborating with another person, or as what you might do if you were using a git repo on two different computers (say, your work computer and your laptop at home). 

We can simulate working with a collaborator using another copy of the repository on our local machine.
To do this,
`cd` to the directory `/tmp`.
(Note the absolute path:
don't make `tmp` a subdirectory of the existing repository).
Instead of creating a new repository here with `git init`,
we will `git clone` the existing repository from GitHub:

~~~
$ cd /tmp
$ git clone https://github.com/vlad/planets.git
~~~
{:class="in"}

`git clone` creates a fresh local copy of a remote repository.
(We did it in `/tmp` or some other directory so that we don't overwrite our existing `planets` directory.)
Our computer now has two copies of the repository:

![After Creating Clone of Repository](fig/git-after-duplicate-clone.svg)

Let's make a change in the copy in `/tmp/planets`:

~~~
$ cd /tmp/planets
$ nano pluto.txt
$ cat pluto.txt
~~~
{:class="in"}
~~~
It is so a planet!
~~~
{:class="out"}
~~~
$ git add pluto.txt
$ git commit -m "Some notes about Pluto"
~~~
{:class="in"}
~~~
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~
{:class="out"}

then push the change to GitHub:

~~~
$ git push origin master
~~~
{:class="in"}
~~~
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/vlad/planets.git
   9272da5..29aba7c  master -> master
~~~
{:class="out"}

Note that we didn't have to create a remote called `origin`:
Git does this automatically,
using that name,
when we clone a repository.
(This is why `origin` was a sensible choice earlier
when we were setting up remotes by hand.)


Our three repositories now look like this:

![After Pushing Change from Duplicate Repository](fig/git-after-change-to-duplicate-repo.svg)

We can now download changes into the original repository on our machine:

~~~
$ cd ~/planets
$ git pull origin master
~~~
{:class="in"}
~~~
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~
{:class="out"}

which gives us this:

![After Pulling Change to Local Repository](fig/git-after-pulling-to-local-repo.svg)

In practice,
we would probably never have two copies of the same remote repository
on our laptop at once.
Instead,
one of those copies would be on our laptop,
and the other on a lab machine,
or on someone else's computer.
Pushing and pulling changes gives us a reliable way
to share work between different people and machines.
