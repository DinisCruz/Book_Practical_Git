##  Fixing the Merge conflict caused by one extra commit on TeamMentor master 

On the 3.4 Release of [TeamMentor](https://teammentor.net/) (which was the first release we really used [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/) on development (see this great presentation on [Git Branching Model](http://blog.diniscruz.com/2013/05/great-presentation-on-git-branching.html)) we ended up with a situation where the commit that was the parent of all feature/fix branches was off-by-one the master of the [TeamMentor/Master](https://github.com/TeamMentor/Master) repository (we also had to do a bunch of back-porting of fixes into that commit, see [Git Flow - Moving patches from one Commit into another Commit post](http://blog.diniscruz.com/2013/09/git-flow-moving-patches-from-one-commit.html))

In practice this means that the [TeamMentor/Master](https://github.com/TeamMentor/Master) graph currently looks like this:  
  
[![image](images/image_thumb_25255B4_25255D1.png)](http://lh3.ggpht.com/-TwP_Fzl0AFk/UkwmmWqhxiI/AAAAAAAAQuE/oUlPVb-Xi7U/s1600-h/image%25255B14%25255D.png)

... with the master branch on the commit **fe26934d489e65660bd67be7811effcbccad1d19**  

[![image](images/image_thumb_25255B5_25255D1.png)](http://lh6.ggpht.com/-YTarBTx-0TY/Ukwmnffgm-I/AAAAAAAAQuU/D4wjyHW1-wA/s1600-h/image%25255B17%25255D.png) 

.. .and the 3_3_3_Hotfix branch on commit **b97a470ffa173d67a9c74373593eea03eb7a2da4**  

[![image](images/image_thumb_25255B6_25255D1.png)](http://lh6.ggpht.com/-HSNVl1QGCBk/Ukwmonc_HvI/AAAAAAAAQug/bxV7DbmwEas/s1600-h/image%25255B20%25255D.png)

But looking at the [TeamMentor/Dev](https://github.com/TeamMentor/Dev/) Graph

[![image](images/image_thumb_25255B7_25255D1.png)](http://lh3.ggpht.com/-QQoUs9DHJZI/Ukwmpazlq3I/AAAAAAAAQu0/608GEa-pfyc/s1600-h/image%25255B23%25255D.png)

...we can see that all commits (done on 'one branch per issue' workflow) have the **b97a470ffa173d67a9c74373593eea03eb7a2da4** commit as its parent (see image above and below)

[![image](images/image_thumb_25255B8_25255D1.png)](http://lh3.ggpht.com/-qKl-uodo2tE/Ukwmqet13mI/AAAAAAAAQvE/_o1_PhEJ3PE/s1600-h/image%25255B26%25255D.png)

In practice this means that the final 3.4 release commit from the [TeamMentor/Dev](https://github.com/TeamMentor/Dev/) repo

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh5.ggpht.com/-G9pESUKo9qc/UkwmrZKTOiI/AAAAAAAAQvU/wz0jtw4LVbI/s1600-h/image%25255B29%25255D.png)

... is incompatible with the [TeamMentor/Master](https://github.com/TeamMentor/Master) repo (note that these could be branches of the same repo, but I like the use of separate repositories, since they provide a nice air-gap between development and production repositories)

Actually in principle they could be merged automatically if there was no conflicts!

But if we look at that extra commit from [TeamMentor/Master](https://github.com/TeamMentor/Master) repo (the [fe26934d489e65660bd67be7811effcbccad1d19](https://github.com/TeamMentor/Master/commit/fe26934d489e65660bd67be7811effcbccad1d19) one)

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh3.ggpht.com/-vcUyUxj5ZFA/Ukwmsh58rKI/AAAAAAAAQvk/aNTlVpxZymA/s1600-h/image%25255B32%25255D.png)

... we see that the change was made on the version number (which in the 3.4 release will now say 3.4)

Note that GitHub will not allow a Pull Request to be made in cases like this, since GitHub has no online merge capabilities.

**Ok, so how do we solve this?**  

The solution is to:  


  1. create a local branch pointing to **b97a470ffa173d67a9c74373593eea03eb7a2da4**
  2. do a pull from [TeamMentor/Master](https://github.com/TeamMentor/Master) to get the [fe26934d489e65660bd67be7811effcbccad1d19](https://github.com/TeamMentor/Master/commit/fe26934d489e65660bd67be7811effcbccad1d19) commit
  3. merge the current 3.4 code into [fe26934d489e65660bd67be7811effcbccad1d19](https://github.com/TeamMentor/Master/commit/fe26934d489e65660bd67be7811effcbccad1d19) (which will cause a conflict)
  4. solve the conflict, 
  5. commit the result
  6. push to GitHub into a new branch (called 3.4_Merge)
  7. do a pull request (from 3.4_Merge into master)

  
In a local clone of [TeamMentor/Dev](https://github.com/TeamMentor/Dev/)   we start by to create a branch that is pointing to **b97a470ffa173d67a9c74373593eea03eb7a2da4**   

This can be done using the command: **$ git checkout **b97a470ffa173d67a9c74373593eea03eb7a2da4** **  

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh5.ggpht.com/-ZAwTGhwLErM/UkwmthpOiBI/AAAAAAAAQv0/NF8ob46Bxp8/s1600-h/image%25255B38%25255D.png)

Followed by (as the help says) with: **$ git checkout -b 3.4_Merge**  

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh5.ggpht.com/-at7Qaj-dnPY/UkwmutoqfCI/AAAAAAAAQwA/kPY0jFMyCRs/s1600-h/image%25255B47%25255D.png)

Next we do a pull from TeamMentor/Master using **$ git pull git@github.com:TeamMentor/Master.git master:3.4_Merge**  

[![image](images/image_thumb_25255B16_25255D1.png)](http://lh5.ggpht.com/-aGtQhK0S1ek/UkwmvqmeVOI/AAAAAAAAQwU/AcNR31rDmLs/s1600-h/image%25255B50%25255D.png)

The command above is basically saying:

_Go to the **git@github.com:TeamMentor/Master.git** repo and merge/add the commits from its **master** branch into the local **3.4_Merge** branch_

Note how the line **_b97a470..fe26934  master     -> 3.4_Merge _**(from screenshot above) shows how we went form the **b97a470ffa173d67a9c74373593eea03eb7a2da4** commit to the **fe26934d489e65660bd67be7811effcbccad1d19 **commit

Next we merge into the **_3.4_Merge_** branch, the contents of the **master** branch (which contains the 3.4 code) using: **$ git merge master**  

[![image](images/image_thumb_25255B17_25255D1.png)](http://lh3.ggpht.com/-eEZenJLIRBw/UkwmwnkgX4I/AAAAAAAAQwk/LZuZnygwK-E/s1600-h/image%25255B53%25255D.png)

.... which predictably failed with a conflict on **_Settings.js_**  

**Solving git conflicts**  

My preferred UI to solve conflicts is the one provided by TortoiseGit, which you can access from here:

[![image](images/image_thumb_25255B26_25255D1.png)](http://lh6.ggpht.com/-oQ2k-lH1aCU/UkwmyJlVtbI/AAAAAAAAQw0/7lphfLyWhzk/s1600-h/image%25255B57%25255D.png)

... them on the popup window that shows up, double click on the conflicted file:

[![image](images/image_thumb_25255B27_25255D1.png)](http://lh5.ggpht.com/-OKCozpkLkd4/UkwmzR7bwyI/AAAAAAAAQxE/l5RlnYV1J2E/s1600-h/image%25255B60%25255D.png)

... and on the TortoiseMerge GUI :

[![image](images/image_thumb_25255B28_25255D1.png)](http://lh4.ggpht.com/-1Af4X_UkhkI/Ukwm0QL-WDI/AAAAAAAAQxU/GmFTRoAVJxE/s1600-h/image%25255B63%25255D.png)

... chose the option to **_Use 'theirs' text block_**  

[![image](images/image_thumb_25255B33_25255D1.png)](http://lh4.ggpht.com/-CnPnrZW4iyU/Ukwm1nV1wcI/AAAAAAAAQxk/0XVYs1EkGt0/s1600-h/image%25255B67%25255D.png)

... which will update the bottom pane with the fixed version of Settings.js (in this case with no changes from before)

[![image](images/image_thumb_25255B34_25255D1.png)](http://lh4.ggpht.com/-YkdjiVy1KiI/Ukwm27ToGLI/AAAAAAAAQx0/4d6JkAiBrFs/s1600-h/image%25255B70%25255D.png)

Save the changes and chose yes to mark the file as resolved:

[![image](images/image_thumb_25255B35_25255D1.png)](http://lh6.ggpht.com/-CbBtFPnFUWk/Ukwm4PmxXUI/AAAAAAAAQyE/CmyIIBfSjOs/s1600-h/image%25255B73%25255D.png)

Close the TortoiseMerge and (since there is no other conflicts) click OK on the Resolve GUI 

[![image](images/image_thumb_25255B36_25255D1.png)](http://lh5.ggpht.com/-CaVf20Oo1oY/Ukwm5DDwJxI/AAAAAAAAQyU/CwoKAnb3eUk/s1600-h/image%25255B76%25255D.png)

... another OK:

[![image](images/image_thumb_25255B37_25255D1.png)](http://lh3.ggpht.com/-T6MzYaFVSO0/Ukwm6OVyusI/AAAAAAAAQyk/fo7vdao-k-0/s1600-h/image%25255B79%25255D.png)

As the multiple 'notes' in the previous UIs mention, we need to commit the changes.

This commit will contain all changes including the conflict fixes

[![image](images/image_thumb_25255B39_25255D1.png)](http://lh3.ggpht.com/-_WXd3HWt7_I/Ukwm8VkFzQI/AAAAAAAAQzE/Q7pBrssuJ68/s1600-h/image%25255B85%25255D.png)

Once the commit is done:

[![image](images/image_thumb_25255B40_25255D1.png)](http://lh5.ggpht.com/-aQDfxWhNmpI/Ukwm99BBOpI/AAAAAAAAQzQ/buOHly6x4Ck/s1600-h/image%25255B88%25255D.png)

Go back to the Git Bash and push this branch into TeamMentor/Master (I prefer to do these things on a Git Bash)

[![image](images/image_thumb_25255B41_25255D1.png)](http://lh3.ggpht.com/-N-N5bxkXvco/Ukwm-hWkNTI/AAAAAAAAQzk/wke8xZYkU6A/s1600-h/image%25255B91%25255D.png)

After the push, this is what the TeamMentor/Master graph looks like:

[![image](images/image_thumb_25255B42_25255D1.png)](http://lh6.ggpht.com/-VvGMd_COknY/Ukwm_xLOfFI/AAAAAAAAQz0/7I05uSxEX4E/s1600-h/image%25255B94%25255D.png)

...with the 3.4 code now being there:

[![image](images/image_thumb_25255B43_25255D1.png)](http://lh4.ggpht.com/-nHHT6DsWs6g/UkwnA9NgFHI/AAAAAAAAQ0E/h7H7zT07wJ4/s1600-h/image%25255B97%25255D.png)

Finally, what we can do now is to issue a Pull Request:

[![image](images/image_thumb_25255B44_25255D1.png)](http://lh4.ggpht.com/-pSLnFrBLdBQ/UkwnB9ZM3iI/AAAAAAAAQ0U/IjVFYFqmr7E/s1600-h/image%25255B100%25255D.png)

... from the**_ 3.4_Merge_** branch:

[![image](images/image_thumb_25255B45_25255D1.png)](http://lh3.ggpht.com/-lga5pisjhLA/UkwnCuoATBI/AAAAAAAAQ0k/Ptw2g3_4urY/s1600-h/image%25255B103%25255D.png)

... into the master branch:

[![image](images/image_thumb_25255B46_25255D1.png)](http://lh4.ggpht.com/-8rwzT_mg4WI/UkwnD9XgDmI/AAAAAAAAQ0w/vpVJaEXNxWY/s1600-h/image%25255B106%25255D.png)

... which contain all the code changes since the 3.3.3 release

[![image](images/image_thumb_25255B47_25255D1.png)](http://lh5.ggpht.com/-i4XiUcK7nyg/UkwnE3yBnxI/AAAAAAAAQ1E/RpHNUDG_sb4/s1600-h/image%25255B109%25255D.png)

With the best part being that this Pull Request can be merged using GitHub's UI (since there are no conflicts)

[![image](images/image_thumb_25255B48_25255D1.png)](http://lh3.ggpht.com/-eSJXRh2zKbU/UkwnFzsnhaI/AAAAAAAAQ1U/FTyUD17ZbbE/s1600-h/image%25255B112%25255D.png)

And that's it!

Hopefully this provided a good example of how to use Git and TortoiseGit to easily merge commits and resolve any resulting conflicts.

  
**Tip: How to delete branches in GitHub:**  

To delete a branch in Github, we do a push from an 'empty branch' into an 'existing branch'

In this case, if I wanted to delete the 3.4_Merge branch at the TeamMentor/Master repository, I would use: 

    $ git push git@github.com:TeamMentor/Master.git :3.4_Merge





- - - 
[Table of Contents](../Table_of_Contents.md)
