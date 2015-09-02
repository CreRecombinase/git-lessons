---
layout: page
title: Version Control with Git
subtitle: Branching
minutes: 20?
---
> ## Learning Objectives {.objectives}
>
> *   Explain what branches are and how you might use them in your research.
> *   Create an experimental branch and merge it back in to the master branch.

Often you may want to test out a new feature in some code. You may or may not decide you want to keep this feature and in the mean time you want to make sure you have a version of your script you know works. [Branches](reference#branches) are instances of a repository that can be edited and version controlled in parallel. You can think of it like making an entire copy of your repository folder that you can edit, without affecting the original versions of your scripts. The advantage of using git to do this (rather that making a repo_copy folder on your computer), is that you can use git tools to manage this code while it's under development and you have the ability to seamlessly merge in your changes to your originals.  

To see what branches are available in your repository, you can type `git branch`. First let's make sure we are all in the planets directory in our home folder:

~~~ {.bash}
$ cd ~/planets
$ git branch
~~~

~~~ {.output}
* master
~~~

The master branch is created with the repository is initialized. With an argument, the `branch` command creates a new branch with the given name. Let's make a new experimental branch:

~~~ {.bash}
$ git branch experimental
~~~

~~~ {.output}
  experimental
* master
~~~

The star indicates we are currently in the master branch of our repository. To switch branches, we use the `git checkout` command to checkout a different branch. 

~~~ {.bash}
$ git checkout experimental
$ git branch
~~~

~~~ {.output}
Switched to branch 'experimental'

* experimental
  master
~~~

We have some updated information on pluto, but we aren't sure that we will want to include in our final report. Let's make some updates to the `pluto.txt` file in this experimental branch:

~~~ {.bash}
$ nano pluto.txt
$ cat pluto.txt
~~~

~~~ {.output}
It is so a planet!
A planet with a charming heart on its surface; What's not to love?
~~~

We've made this change on our experimental branch. Let's add and commit this change:

~~~ {.bash}
$ git add pluto.txt
$ git commit -m "Breaking updates about Pluto"
~~~

~~~ {.output}
[experimental c5d6cba] Breaking updates about Pluto
 1 file changed, 1 insertion(+)
~~~

Let's check our status:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
On branch experimental
nothing to commit, working directory clean
~~~

You can see from the git status output that we are on the experimental branch rather than the master branch. Let's examine the master branch to ensure the original version of our `pluto.txt` doesn't include this sentimental statement:

~~~ {.bash}
$ git checkout master
~~~

~~~ {.output}
Switched to branch 'master'
~~~

~~~ {.bash}
$ cat pluto.txt
~~~

~~~ {.output}
It is so a planet!
~~~

As you can see, the master branch does not include our updated notes about Pluto. We are pretty confident that the heart in Pluto is charming, so let's fold in all of the changes that we've made on the experimental branch into our master branch. To merge two branches together, ensure you are located in the branch you want to fold changes into. In our case, we want to be in the master branch:

~~~ {.bash}
$ git branch
~~~

~~~ {.output}
  experimental
* master
~~~

Excellent, we are in the right place. To fold the experimental branch into the master branch, we use the `merge` function of git followed by the name of the branch we want to fold in:

~~~ {.bash}
$ git merge experimental
~~~

~~~ {.output}
Updating ee530d7..c5d6cba
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
~~~

Now if we look at our `pluto.txt` file, we see our updates from the experimental branch:

~~~ {.bash}
$ cat pluto.txt
~~~

~~~ {.output}
It is so a planet!
A planet with a charming heart on its surface; What's not to love?
~~~

Now let's push all these changes up to github:

~~~ {.bash}
$ git push --all origin
~~~

~~~ {.output}
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 348 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To https://github.com/erdavenport/planets.git
   4959da7..a822910  master -> master
 * [new branch]      experimental -> experimental
~~~

Branches can be difficult to visualize in your head. GitHub has a nice feature that will let you examine your commits on each branch. Find the graphs link of your repository home page:

![Locating Graphs on GitHub](fig/github-find-graphs-image.png)  

You can see a graphical representation of your commit and branch history here. If you hover your cursor over the dots (commits), a box will display the commit message and ID. Your different branches are shown in different colors, with an arrow indicating when you merged two branches together.

![Viewing Branch and Commit History on GitHub](fig/github-graphs-image.png)

We no longer have a use for our experimental branch. To delete a branch you don't need, you can use the `-d` flag of `git branch`:

~~~ {.bash}
$ git branch -d experimental
~~~

~~~ {.output}
Deleted branch experimental (was c5d6cba).
~~~
