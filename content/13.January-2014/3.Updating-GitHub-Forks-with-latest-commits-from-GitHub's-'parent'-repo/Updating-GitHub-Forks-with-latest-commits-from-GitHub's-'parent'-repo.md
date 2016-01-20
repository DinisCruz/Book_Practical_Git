## Updating GitHub Forks with latest commits from GitHub's 'parent' repo

One of the areas that tend to case some problems with GitHub 'Forking model' workflow, is the need to have the _Forks_ updated with the commits that have been added to the _Parent_ repo (i.e. the repo that was used to create the _Fork_ from).

To see real-word examples (and pains) of this issue, take a look at these posts:  


* [How to update a forked GitHub repo (in this case tm-sme/Lib_Vulnerabilities)](http://blog.diniscruz.com/2014/01/how-to-update-forked-github-repo-in.html)
* [Syncing all releases to the same commit and Tag (for TeamMentor v3.4)](http://blog.diniscruz.com/2013/10/syncing-all-releases-to-same-commit-and.html)
* [Fixing the Merge conflict caused by one extra commit on TeamMentor master](http://blog.diniscruz.com/2013/10/fixing-merge-conflict-caused-by-one.html)

For the example show below, I'm going to update the [DinisCruz-Dev/TeamMentor_Eclipse_Plugin](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin) repo which is a _Fork_ of [TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) (here also referenced as the _Parent_ repo).

At the moment these repos are the stage shown in [Updating the GitHub repos for the 1.6.0 release of the Eclipse Fortify Plugin](http://blog.diniscruz.com/2014/01/updating-github-repos-for-160-release.html) :

* The commits made on the _Fork_ ([DinisCruz-Dev/TeamMentor_Eclipse_Plugin](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin)) have been pushed into the _Parent_ ([TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin)) as a Pull Requests
* All Pull Requests have been merged back into the _Parent_ repo (with even a [v1.6.0 tag created to mark the release](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/releases/tag/1.6.0))
* The _Fork_ repo has NOT been updated with the final commits.

Here is what this looks like form the _Parent's_ repo [TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) point of view:

![](images/Screen_Shot_2014-01-25_at_01_04_12.png)

And here is what this looks like form the _Forked_ repo [DinisCruz-Dev/TeamMentor_Eclipse_Plugin](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin) point of view:

![](images/Screen_Shot_2014-01-25_at_01_06_02.png)

Looking at the common commits, might help to visualize what is going on.

The last commit at the _Fork_ is the  [b4dad953767fcc674d9ca948fc0cfb762415f01c](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/commit/b4dad953767fcc674d9ca948fc0cfb762415f01c), which can be seen below as represented by the large LAST BLUE dot in the [DinisCruz-Dev/TeamMentor_Eclipse_Plugin](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin) repo Network graph

![](images/Screen_Shot_2014-01-25_at_01_49_33.png)

But the same commit can be seen below as the large GREEN dot in the [TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) _Parent_ repo (note that it is not the last one in this repo):  

![](images/Screen_Shot_2014-01-25_at_01_50_10.png)

At the moment the _Parent_ repo is currently at the [2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/commit/2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43) commit (which doesn't exit in the _Forked_ repo)

![](images/Screen_Shot_2014-01-25_at_01_55_29.png)

The practical consequences of this situation, is that the _Fork_ is currently in an 'incompatible' state with its _Parent_ , and it will not be possible to send Pull Requests/code-fixes upstream (note that this is 'by design' since Git does not allow merges when there are no common parents).

The solution is to do a Pull Request from '_Parent_ to _Fork_' (ie. from [TeamMentor/TeamMentor_Eclipse_Plugin](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin) to [DinisCruz-Dev/TeamMentor_Eclipse_Plugin](https://github.com/DinisCruz-Dev/TeamMentor_Eclipse_Plugin)), as seen below:

![](images/Screen_Shot_2014-01-25_at_02_03_03.png)

In this case, there is only one update (made directly on the _Parent_ repo) that needs to be merged into the _Forked_ repo, and more importantly we get the desired [2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/commit/2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43) commit:

![](images/Screen_Shot_2014-01-25_at_02_03_27.png)

Here is how I created the Pull Request:

![](images/Screen_Shot_2014-01-25_at_02_03_53.png)

Which I then opened up in a browser logged in as _DinisCruz-Dev_ (the **_DinisCruz_** account doesn't have GitHub privs to make this merge)

![](images/Screen_Shot_2014-01-25_at_02_04_49.png)

And since the commits are all compatible, I can just click on the 'Merge pull request' button:

![](images/Screen_Shot_2014-01-25_at_02_05_04.png)

... to successfully apply the merge:

![](images/Screen_Shot_2014-01-25_at_02_05_14.png)

And now the Forked repo contains all commits that exist in the 'parent' repo (note the the [2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43](https://github.com/TeamMentor/TeamMentor_Eclipse_Plugin/commit/2ac007c7385fd992fb5f6c6e4774cfdaaa88ba43) commit below)

![](images/Screen_Shot_2014-01-25_at_02_05_38.png)

A final good house cleaning step is to also update the Master branch of the Fork:

![](images/Screen_Shot_2014-01-25_at_02_07_18.png)

... which makes the final version of the graph look like this:

![](images/Screen_Shot_2014-01-25_at_02_08_02.png)

Note that all these steps could had been done using the git.exe command line, and in some cases, that is better, since we have more control over the creation of new commits on merge (for example note how every-time I merged a Pull Request in GitHub, a new commit was created! ... which is something that is not needed all the time)

For example I prefer when we can align the branches that are synced with the same commit, like what was done on [Syncing all releases to the same commit and Tag (for TeamMentor v3.4)](http://blog.diniscruz.com/2013/10/syncing-all-releases-to-same-commit-and.html)  and shown below:

![](images/image_thumb_25255B18_25255D1.png)
