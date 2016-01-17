## Rewriting Git History (locally and at GitHub)

When fixing the [ASP.NET WCF REST help page 'Memory gates checking' error at AppHarbor](http://blog.diniscruz.com/2012/12/problem-with-environmentspecialfolderap.html),

I ended up with a number of Git Commits: locally

![](images/image_thumb_25255B20_25255D.png)

and at GitHub

![](images/image_thumb_25255B18_25255D.png)

Once we found the solution (and pushed a new version of FluentSharp.CoreLib.dll to Nuget), it was time to clean up the history (since those commits don't really need to be in the [main TM master](https://github.com/TeamMentor/Master_3_3)). Yes I could had used a branch, but since this was part of the TeamCity deployment tests, It was useful to do it on the master branch (and see how fast TeamCity can be :)  )

So what we want to do, is to **something that is not very common in Git: rewrite Git's history** (i.e. remove pushed commits). In practice this means that we want to 'go back' to the commit marked in blue (gitk image above) ,and remove the extra commits from the main Git History:

Just in case something goes wrong, lets let's backup the current changes as a local branch :)

![](images/image_thumb_25255B5_25255D.png)

Once that is done, we do a 'forced git reset':

![](images/image_thumb_25255B11_25255D.png)

This does the trick, and now the (local) history looks good:

![](images/image_thumb_25255B9_25255D.png)

and

![](images/image_thumb_25255B10_25255D.png)

Next,  to remove these commits from GitHub ...

![](images/image_thumb_25255B12_25255D.png)

....we do a **_git push --force _**

![](images/image_thumb_25255B13_25255D.png)   

And GitHub's version has been moved back:

![](images/image_thumb_25255B14_25255D.png)

Finally we update ( on the TeamMentor VS Projects) the FluentSharp.CoreLib.dll via NuGet:

![](images/image_thumb_25255B15_25255D.png)

and commit it:

![](images/image_thumb_25255B16_25255D.png)

Creating the desired Git Commit History:

![](images/image_thumb_25255B21_25255D.png)
