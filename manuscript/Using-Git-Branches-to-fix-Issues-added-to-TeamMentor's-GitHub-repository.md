## Using Git Branches to fix Issues added to TeamMentor's GitHub repository

This is the currently workflow that I'm following when coding/fixing TeamMentor Issues added to the [TeamMentor/Master/Issues](https://github.com/TeamMentor/Master/issues) list.  


  * Find issue to address
  * Create and checkout new branch (with the issue ID on its title)
  * Apply the fixes (on the new branch)
  * Commit the changes (on the new branch)
  * Checkout master branch
  * Merge changes (from new branch) into master , using the --no--ff (no fast-forward) option (this is very important, see [here](http://stackoverflow.com/questions/6701292/git-fast-forward-vs-no-fast-forward-merge) and [here](http://stackoverflow.com/questions/2850369/why-does-git-use-fast-forward-merging-by-default/2850413#2850413) for a good explanation why)
  * Push to GitHub

**Lets look at this in action.**  

Here is a simple issue to fix: [https://github.com/TeamMentor/Master/issues/389](https://github.com/TeamMentor/Master/issues/389)

![](images/using-git-branch-1.png)

In GitHub, the issue is #389, so on a local clone of the Master repository, we create a branch called **_Issue_389_** (using the --b switch to create it)

![](images/using-git-branch-2.png)

In VisualStudio, apply the fix to the code:

![](images/using-git-branch-3.png)

Quickly look in a browser to confirm the change (this should also be reconfirmed via a UI UnitTest):

![](images/using-git-branch-4.png)

Commit the change to the **Issue_389** branch:

![](images/using-git-branch-5.png)

Which means that at this moment, there is nothing else to commit on the **_Issue_389_** branch:

![](images/using-git-branch-6.png)

which is now one commit ahead of master

![](images/using-git-branch-7.png)

Next step is to **_checkout _**(into) master and do the **_git merge_** using the **_--no--ff _**

![](images/using-git-branch-8.png)

Gitk shows the effect of the **_--no--ff_** (ie. the use of the branch was preserved)

![](images/using-git-branch-9.png)

Final step is to push the commits to GitHub:

![](images/using-git-branch-10.png)

Here is the commit at GitHub:

![](images/using-git-branch-11.png)

Here is the GitHub's Network view:

![](images/using-git-branch-12.png)
