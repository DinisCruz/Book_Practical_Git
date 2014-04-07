##  Git Flow - Moving patches from one Commit into another Commit 

This (longish) post will cover detailed git workflows and is part of the series of blog posts that show how we use the Git Flow workflow to manage TeamMentor's source code (you will also see practical applications of GitHub's powerful  of powerful features like Network Graphs and Pull Requests).

The key problem that we are going to solve, is the situation created by [Michael Hidalgo](http://blog.michaelhidalgo.info/)'s TeamMentor fixes/commits/branches that were done against an commit (**38bfcd54d8046372c0ace2409324ecc965761504**)** **which was originally planed to be part of the next release, but we decided that the next **_3.4 Release_** of TeamMentor will be based on the current 3.3.3 version (with is based on the earlier commit: **_b97a470ffa173d67a9c74373593eea03eb7a2da4_**).

The key reason is that he  **38bfcd54d8046372c0ace2409324ecc965761504 commit **(currently the parent of Michael's fixes/branches) is not stable and is going now to be the basis of the **_3.5_Release_** (this code contains a number of big changes which need more TLD and testing: native ASP.NET MVC routing, better Git support, native Markdown editor, depreciation of HTML WYSIWYG editor, and more)

In a nutshell, we need to re-apply Michael's bug fixes to an earlier commit than the one used (i.e. backport those commits).

  
To start, here is what Michael's branches look like at the moment (note that all have the **38bfcd54d8046372c0ace2409324ecc965761504  **commit as parent):

[![image](images/image_thumb_25255B8_25255D1.png)](http://lh5.ggpht.com/-zeBWsYq3tj8/UiffWG8pmfI/AAAAAAAAPys/mlDZ2p-A9ZU/s1600-h/image%25255B26%25255D.png)

Here is the commit (**38bfcd54d8046372c0ace2409324ecc965761504) **that we want to have as the parent, since this is the commit that is currently on the 3.3.3. release (and will be the basis for the 3.4 release of TeamMentor):

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh6.ggpht.com/-2sWCenafODI/UiffXvyM8qI/AAAAAAAAPy8/fuk2MGmKwTU/s1600-h/image%25255B29%25255D.png)

Basically, what we need to do is to 'just' backport the branches linked to **38bfcd54d8046372c0ace2409324ecc965761504** commit,  into the  _b97a470ffa173d67a9c74373593eea03eb7a2da4 _commit  
**_  
_**Note: since this post was getting quite long, I moved some workflows into Appendixes (included below) so that the key actions/changes can be read in sequence.

Using the workflow described in the **_Appendix 1) Creating patches from Michael's branches_** here are the patches to apply (i.e. these are all changes from the branches currently available in Michael's dev repository):

[![image](images/image_thumb_25255B33_25255D1.png)](http://lh3.ggpht.com/-udXUXdFyYcI/UiffZDCfqxI/AAAAAAAAPzM/t6sdeO8sSxw/s1600-h/image%25255B101%25255D.png)

After:

  * Fixing the master branch and creating a feature branch for the 3.5_Release (so that **_TeamMentor/Dev_** master branch is in sync with **TeamMentor/Master **master brach, and the 3.5 commits are not lost) 

    * _... see __Appendix 2) Creating a 3.3.3 tag and branch in Dev repository _
    * _... see  **Appendix 4) Creating a 3.5_Release Feature branch** )  
_

  * Applying the 6 patches that merged without conflict 

    * _... see **Appendix 3) Applying patches**_

...we get the following TeamMentor/Dev '_not merged branches'_:

[![image](images/image_thumb_25255B92_25255D.png)](http://lh6.ggpht.com/-zH257IA2QAM/UiffaZ2RVnI/AAAAAAAAPzc/gAfYtFTyIEU/s1600-h/image%25255B241%25255D.png)

After the pull requests are made into a new 3.4_Release branch (see **_Appendix 5) Creating a 3.4_Release Feature branch_ **for more details) we have 5 Issues/branches applied (and ready for QA):

[![image](images/image_thumb_25255B108_25255D.png)](http://lh3.ggpht.com/--clfyaWCj_8/UiffboXVkgI/AAAAAAAAPzs/6nNF8yIe8As/s1600-h/image%25255B289%25255D.png)

Here is the graph view, with **_TeamMentor/Dev _**master (blue line below):

[![image](images/image_thumb_25255B111_25255D.png)](http://lh6.ggpht.com/-rJGPNuuDOoE/UiffdBUi20I/AAAAAAAAPz4/QWlheavU7CY/s1600-h/image%25255B298%25255D.png)

.... now being the parent of the **_Issue_142, Issue_51, Issue_400, Issue_475_** and **_Issue_459_** branches:

[![image](images/image_thumb_25255B109_25255D.png)](http://lh3.ggpht.com/-Cx5Ca-5vHAk/UiffeGE_hzI/AAAAAAAAP0M/TtUxVfEG95E/s1600-h/image%25255B292%25255D.png)

This concludes the (main part of) this post, which showed how to handle the scenario where  fixes (and branches) were applied to a commit whose release schedule was changed (and there was the need to back-port those changes into an earlier commit).

I think it is important to note that the workflow shown in here is a great proof of the power of Git (I can't even image doing this in SVN).

In fact, in this case, we are paying the price for not being more formal in the use of Git Flow workflows, and for not being more strategic on where we applied simple fixes (like the ones shown here).

I.e. this should be easier next time.

That said, it took me orders-of-magnitude more time to write this blog post, than to actually make these changes/fixes :)

**Appendix 1) Creating patches from Michael's branches:**

To create the patches, I grabbed a fresh clone of Michael's dev repo (which is a fork of TeamMentor/Dev)

[![image](images/image_thumb1.png)](http://lh6.ggpht.com/-z8bLmI7kV2A/UifffUu1TpI/AAAAAAAAP0c/zxKlYqW5YNc/s1600-h/image%25255B2%25255D.png)

Then, on a git bash of this repository, I created a new branch that pointed to the current  
**_38bfcd54d8046372c0ace2409324ecc965761504_** commit, using the commands: **_$ git checkout 38bfcd54d8046372c0ace2409324ecc965761504 _**and **_$ git checkout -b Patch_Parent_**  
**_  
_**[![image](images/image_thumb_25255B16_25255D1.png)](http://lh5.ggpht.com/-9G7FeIqgpDk/UiffhK_xgLI/AAAAAAAAP0s/KfJfo_1scYg/s1600-h/image%25255B50%25255D.png)

The reason I picked the **_38bfcd54d8046372c0ace2409324ecc965761504_** commit is because this is the commit that all Michael's current branches are based on:

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh4.ggpht.com/-rFmsd11yLQs/UiffiZK7-WI/AAAAAAAAP08/qlFX_bKRiq4/s1600-h/image%25255B47%25255D.png)

Using the **$ git branch -a **command, we can see that this local repository/clone already contains the branches we need:

[![image](images/image_thumb_25255B11_25255D1.png)](http://lh4.ggpht.com/-tyydaL51Zmo/UiffjgYaD1I/AAAAAAAAP1M/GBkDGtVy9mA/s1600-h/image%25255B35%25255D.png)

Let's start with a simple one, for example the changes on [Issue 534](https://github.com/TeamMentor/Master/issues/534):

[![image](images/image_thumb_25255B13_25255D1.png)](http://lh3.ggpht.com/-sWnVS4PZ5ks/Uiffk0Kw64I/AAAAAAAAP1c/a4LABEuesL4/s1600-h/image%25255B41%25255D.png)

whose changes are on branch **_Issue_534_**  
**_  
_**[![image](images/image_thumb_25255B12_25255D1.png)](http://lh6.ggpht.com/-wY39ub618KE/UiffmpVg6eI/AAAAAAAAP1s/KABc7joCxYg/s1600-h/image%25255B38%25255D.png)

In order to create the patch, I created a local tracking branch using the command **_$ git checkout -b Issue_534 remotes/origin/Issue_534_**  
**  
**[![image](images/image_thumb_25255B20_25255D1.png)](http://lh5.ggpht.com/-sSPeMnib3h8/UiffnxZKBCI/AAAAAAAAP18/Ws7QnF-L4gQ/s1600-h/image%25255B62%25255D.png)

I then created a patch using **_$ git format-patch Patch_Parent_**  
**  
**[![image](images/image_thumb_25255B21_25255D1.png)](http://lh3.ggpht.com/-oIwNUmlSDog/UiffpASz00I/AAAAAAAAP2M/IggM6gsAtQc/s1600-h/image%25255B65%25255D.png)

...which created the file **_0001-Fixing-Issue_534.patch_**:

[![image](images/image_thumb_25255B23_25255D1.png)](http://lh5.ggpht.com/-Ve8Wjh5E-Rk/UiffqF7lIAI/AAAAAAAAP2c/GrjEg7yuCcs/s1600-h/image%25255B71%25255D.png)

... containing these changes:

[![image](images/image_thumb_25255B24_25255D1.png)](http://lh6.ggpht.com/-wrT30M5rEGk/UiffrkNEFXI/AAAAAAAAP2s/mKLuYE43Ab0/s1600-h/image%25255B74%25255D.png) 

...the these ones:

[![image](images/image_thumb_25255B25_25255D1.png)](http://lh6.ggpht.com/-oN_ELO6nfbE/Uiffs0jDfGI/AAAAAAAAP28/hEHtxSoohRA/s1600-h/image%25255B77%25255D.png)

Note: the reason the patch is about 1Mb is because Michael (on this branch) also committed a bunch of *.dlls which should not be there.

One more little thing, since we are going to create a number of these patch files, it is better to put them on a dedicated folder. This can can be done using the command: **_$ git format-patch Patch_Parent -o ../_3.4_Patches_**  
**_  
_**[![image](images/image_thumb_25255B26_25255D1.png)](http://lh4.ggpht.com/-lX678QEu4CA/Uiffuo-m_5I/AAAAAAAAP3M/b0J0WZ4v0-4/s1600-h/image%25255B80%25255D.png)

... with the _'patch file'_ now being placed on the folder:

[![image](images/image_thumb_25255B27_25255D1.png)](http://lh6.ggpht.com/-ZJ2xMLB3GNY/Uiffv64f6-I/AAAAAAAAP3c/05yQTmXhbbU/s1600-h/image%25255B83%25255D.png)

Here is the same process for Issue_565:

[![image](images/image_thumb_25255B28_25255D1.png)](http://lh6.ggpht.com/-ew_LBEI-dhw/UiffxC5Cq0I/AAAAAAAAP3s/Uqs7KgUWHro/s1600-h/image%25255B86%25255D.png)

... with the patch created in:

[![image](images/image_thumb_25255B29_25255D1.png)](http://lh6.ggpht.com/-PmK00mUc0IE/UiffyJheRWI/AAAAAAAAP38/Lz0uxa1mWDE/s1600-h/image%25255B89%25255D.png)

We can also create the patches without creating a tracking branch. For example here is how to create a patch for the code at the Issue_51 branch:

[![image](images/image_thumb_25255B30_25255D1.png)](http://lh4.ggpht.com/-7ly-w32drXA/UiffzdBLjVI/AAAAAAAAP4M/3bGapfSPXXw/s1600-h/image%25255B92%25255D.png)

Note that the _0001-Fixing-Issue-51.patch _file is much smaller (3k) then the others

[![image](images/image_thumb_25255B31_25255D1.png)](http://lh5.ggpht.com/-4296r_ZwFS4/Uiff0prbxII/AAAAAAAAP4c/-hBTNQIMcWs/s1600-h/image%25255B95%25255D.png)

This is caused by this patch only containing text diffs (and no binaries), which is how all patches should be:

[![image](images/image_thumb_25255B32_25255D1.png)](http://lh6.ggpht.com/-bCngLadt3ug/Uiff2OD269I/AAAAAAAAP4s/mumUlDYff1E/s1600-h/image%25255B98%25255D.png)

Finally here are all the patch files created (containing all commits made by Michael's branches):

[![image](images/image_thumb_25255B33_25255D1.png)](http://lh3.ggpht.com/-udXUXdFyYcI/UiffZDCfqxI/AAAAAAAAPzM/t6sdeO8sSxw/s1600-h/image%25255B101%25255D.png)   
**  
****  
****Appendix 2) Creating a 3.3.3 tag and branch in the _TeamMentor/Dev_ repository **  
**  
**In order to be able to apply the changes into the _TeamMentor/Master _master branch, I created a branch in the current **_TeamMentor/Dev_** that points to the last common commit between**_ TeamMentor/Master_** and **_TeamMentor/Dev_** (this way the commits can be pushed into **TeamMentor/Master **master_ _branch, and eventually pulled into the **_TeamMentor/Dev _**3.5_Release branch)

Since **_b97a470ffa173d67a9c74373593eea03eb7a2da4_**  is the last commit in **_TeamMentor/Master_** that also exists in _**TeamMentor/Dev**, _we are we are going to use as the parent for the patches/branches to apply:

[![image](images/image_thumb_25255B4_25255D1.png)](http://lh6.ggpht.com/-pdad-Ri_TYs/Uiff3fI1IbI/AAAAAAAAP48/vF8awVea7Uc/s1600-h/image%25255B14%25255D.png)

To do so, I started by opening up my local dev repo (currently in sync with the latest commit to Dev) , and executed **_$ git checkout b97a470ffa173d67a9c74373593eea03eb7a2da4_**   
**_  
_**[![image](images/image_thumb_25255B3_25255D1.png)](http://lh4.ggpht.com/-YxKMyXalQI8/Uiff4rKqolI/AAAAAAAAP5M/ah0UxLrFyDU/s1600-h/image%25255B11%25255D.png)

I then created a tracking branch (called 3.3.3_Release) and added a tag (called v3.3.3), using the commands: **_$ git checkout -b 3.3.3_Release_** and **_$ git tag -a v3.3.3  -m '3.3.3_ Release'**  
**  
**[![image](images/image_thumb_25255B5_25255D1.png)](http://lh6.ggpht.com/-I4QZi0Zxyf4/Uiff511HEMI/AAAAAAAAP5Y/Kc5H0xwRlMA/s1600-h/image%25255B17%25255D.png)

I then pushed the _**3.3.3_Release**_ branch and **_v3.3.3_** tag into the **_TeamMentor/Dev_** repository, using the commands: **_$ git push dev 3.3.3_Release:3.3.3_Release_ **and **_$ git push dev v3.3.3_**  
**_  
_**[![image](images/image_thumb_25255B6_25255D1.png)](http://lh5.ggpht.com/-8PgM4KEhIOk/Uiff6_9aiuI/AAAAAAAAP5s/ibG-a0b5X64/s1600-h/image%25255B20%25255D.png)

Following these commands (and without the pushes that will happen next) we can see the **_3.3.3_Release_** tag in **_TeamMentor/Dev_** network graph  
[![image](images/image_thumb_25255B1_25255D1.png)](http://lh4.ggpht.com/-rdz0vn_VSWM/Uiff8Dnc3BI/AAAAAAAAP58/gArS5NvV1s8/s1600-h/image%25255B5%25255D.png)

  
**Appendix 3) Applying patches**  
**  
**We are now going to apply the patches files (previously created), into the 3.3.3_Release branch of the current local clone of **_TeamMentor/Dev_**

[![image](images/image_thumb_25255B36_25255D1.png)](http://lh3.ggpht.com/-ytIbhrWfa78/Uiff9grp-WI/AAAAAAAAP6I/Aentzn9HI0k/s1600-h/image%25255B110%25255D.png)

Starting with the **_0001-Fixing-Issue_142.patch_** which is a simple change:

[![image](images/image_thumb_25255B38_25255D1.png)](http://lh4.ggpht.com/-z6dhTunqaSc/UifgCnXu3DI/AAAAAAAAP6c/B_xkhAFCmrs/s1600-h/image%25255B116%25255D.png)

To get a preview of what will change when we apply a patch, we can use the command: **_$ git apply --stat ../_3.4_Patches/0001-Fixing-Issue_142.patch_**  
**_  
_**[![image](images/image_thumb_25255B39_25255D1.png)](http://lh4.ggpht.com/-7LgKuWQwR-I/UifgEP2wuTI/AAAAAAAAP6s/gSp17Fi-iOA/s1600-h/image%25255B119%25255D.png)

To see if we are going to have any errors when applying a patch, we can use the  command: **$ git apply --check ../_3.4_Patches/0001-Fixing-Issue_142.patch **  
**  
**[![image](images/image_thumb_25255B41_25255D1.png)](http://lh4.ggpht.com/-MmuXHy-Q3f8/UifgFd_7pRI/AAAAAAAAP68/Z63CnFVFQ2U/s1600-h/image%25255B125%25255D.png)

In this case, the fact that we saw no messages on the **---check** command (shown above), means that we can merge this patch file ok:

[![image](images/image_thumb_25255B42_25255D1.png)](http://lh5.ggpht.com/-Tx3xsn4VYn4/UifgGt0juSI/AAAAAAAAP7M/YWqxkiXcrdc/s1600-h/image%25255B128%25255D.png)

... in this case the change was applied on top of our current branch code (with no commit added)

[![image](images/image_thumb_25255B43_25255D1.png)](http://lh5.ggpht.com/-SC6644OAf3Y/UifgIE4d0RI/AAAAAAAAP7c/xgr0RW1cFI8/s1600-h/image%25255B131%25255D.png)

But that has the problem that there was no commit made (just the files changed on disk).

Since we want to preserve the original commit we, will need to can use another command.

First lets reset the current change:

[![image](images/image_thumb_25255B49_25255D.png)](http://lh5.ggpht.com/-QJFw_Wujic8/UifgJaywSyI/AAAAAAAAP7s/8tvCqe0Yy_o/s1600-h/image%25255B135%25255D.png)

... and before we apply the **0001-Fixing-Issue_142.patch**,** **lets create the Issue_142 branch, using the command **git checkout --b Issue_142**  
**  
**[![image](images/image_thumb_25255B53_25255D1.png)](http://lh4.ggpht.com/-g1x3jI2MSJE/UifgKZ6fTXI/AAAAAAAAP78/pO9ksEDL5Y0/s1600-h/image%25255B147%25255D.png)

Now lets apply the patch this using the command: **_$ git am --signoff < ../_3.4_Patches/0001-Fixing-Issue_142.patch_**  
**_  
_**[![image](images/image_thumb_25255B54_25255D1.png)](http://lh6.ggpht.com/-qHleRqpQ6YU/UifgLVDNl-I/AAAAAAAAP8M/K5h9v8hlHkk/s1600-h/image%25255B150%25255D.png)

...which will add a commit containing the original commit message and author:

[![image](images/image_thumb_25255B55_25255D1.png)](http://lh4.ggpht.com/-aQ5QNZpLuKo/UifgMtqyqnI/AAAAAAAAP8c/9RznQCNFjfE/s1600-h/image%25255B153%25255D.png)

Next we push this branch into TeamMentor/Dev

[![image](images/image_thumb_25255B57_25255D1.png)](http://lh4.ggpht.com/-lCUOoadokOY/UifgNkWiNsI/AAAAAAAAP8s/Yk1kDqlhAoA/s1600-h/image%25255B159%25255D.png)

And confirm that the Issue_142 changes are in the correct location (i.e with the **_b97a470ffa173d67a9c74373593eea03eb7a2da4_**  commit as its parent):

[![image](images/image_thumb_25255B58_25255D1.png)](http://lh4.ggpht.com/-hlE7yZJphg4/UifgOwWF_UI/AAAAAAAAP88/mlxS22i5mHI/s1600-h/image%25255B162%25255D.png)

Note how the light blue line is connected from the **_b97a470ffa173d67a9c74373593eea03eb7a2da4_**  commit (see above) into the newly pushed **5319e3028da01c64d09409b833c4f33bc49b7208 **commit (see below)

[![image](images/image_thumb_25255B59_25255D1.png)](http://lh4.ggpht.com/-XgUUZH1R84g/UifgP0Px5ZI/AAAAAAAAP9M/resXnzi6bRg/s1600-h/image%25255B165%25255D.png)

... which is the current head of the **Issue_142** branch

[![image](images/image_thumb_25255B60_25255D1.png)](http://lh3.ggpht.com/-qf_dZsbhi4I/UifgRCqPneI/AAAAAAAAP9c/IIK7vhgRfWI/s1600-h/image%25255B168%25255D.png)

The next image shows how we can use GitHub's UI to create/view the pull request for this branch:

  
[![image](images/image_thumb_25255B61_25255D1.png)](http://lh5.ggpht.com/--UMrjjZefhI/UifgSMetU6I/AAAAAAAAP9s/EGpsVteFgmA/s1600-h/image%25255B171%25255D.png)

Note how in the screenshot above the **_Issue_142_** branch is 129x commit behind master.

That is caused by the fact that master is currently at the commit **16354b3ec1757f56f0ee1594de3c72bb506f6537** and it should be at the commit **b97a470ffa173d67a9c74373593eea03eb7a2da4 **  
**  
**See **_Appendix 5) Creating a 3.4_Release Feature branch and merging branches _**for how that was fixed.

After mapping the current master commit into a new the 3.5_Release branch and doing a force reset to the master branch, we get the **_Issue_142_** branch correctly set-up with 1x commits ahead and 0x commits behind the master branch:

[![image](images/image_thumb_25255B87_25255D.png)](http://lh4.ggpht.com/-4sMiOBKulo0/UifgTYzDlGI/AAAAAAAAP98/8lBIDjuCNZY/s1600-h/image%25255B226%25255D.png)

With TeamMentor/Dev master branch in the correct location, lets apply more patches into it:

For example Issue 51, using the commands:  


> **$ git apply --check ../_3.4_Patches/0001-Fixing-Issue-51.patch  **(check if patch can be applied)  
**$ git checkout -b Issue_51                                                              **(create patch branch)  
**$ git am --signoff < ../_3.4_Patches/0001-Fixing-Issue-51.patch**  (apply patch and preserve original commit)  
**$ git push dev Issue_51:Issue_51                                                  **(push branch into GitHub)

[![image](images/image_thumb_25255B89_25255D.png)](http://lh6.ggpht.com/-l_ySjoQC78k/UifgUdr11uI/AAAAAAAAP-M/l6tYOOclfq4/s1600-h/image%25255B232%25255D.png)

This makes the **_Issue_51_** branch to also be 1x ahead and 0x behind commits of the master branch:

[![image](images/image_thumb_25255B90_25255D.png)](http://lh4.ggpht.com/-hpLg2ZAOpvY/UifgV37RvZI/AAAAAAAAP-Y/PHQGC7alXoU/s1600-h/image%25255B235%25255D.png)

With this workflow in place, I quickly did the same workflow for the branches: **Issue_384 , Issue_400 , Issue_475** and **Issue_459**  
**  
**At the moment we have these branches to merge (_Appendix 5) Creating a 3.4_Release Feature branch and merging branches _will show them in action):

[![image](images/image_thumb_25255B91_25255D.png)](http://lh5.ggpht.com/-flRniOAbEYY/UifgW8Nyd3I/AAAAAAAAP-s/9tKRpMCpC4I/s1600-h/image%25255B238%25255D.png)

Note that there were numerous patches (534, 565, 193, 285, 461, 517, 504, 527,462 and 445) that didn't merge correctly.

For example this is what happened for the **0001-Fixing-Issue-565.patch **when executing the command **$ git apply --check ../_3.4_Patches/0001-Fixing-Issue-565.patch **  
**  
**[![image](images/image_thumb_25255B37_25255D1.png)](http://lh5.ggpht.com/-ihq9GL-Z-10/UifgYBjxoVI/AAAAAAAAP-8/AJUUKmkvGIc/s1600-h/image%25255B113%25255D.png)

These will need to be handled separately (which is a topic for another blog post, since this one is already getting a bit long :) )

  
**Appendix 4) Creating a 3.5_Release Feature branch**

In order to make the current **_TeamMentor/Dev_** match the **_TeamMentor/Master_** in terms of the master branch, we need to move the current master of **_TeamMentor/Dev_** into a feature branch called **_3.5_Release_** (in a way we were using the master of **_TeamMentor/Dev_** as a 'feature branch' which was ok if that code was going to become the 3.4 release (which now it isn't).

First step is to move into the current master using the command **_$ git checkout master_**  
**_  
_**[![image](images/image_thumb_25255B63_25255D.png)](http://lh5.ggpht.com/-Ka78hdEXAY0/Uifgtnf7FhI/AAAAAAAAP_M/jSUFp8gDKtQ/s1600-h/image%25255B177%25255D.png)

Then we create the 3.5_Release feature branch using the command **_$ git checkout --b 3.5_Release_**  
**_  
_**[![image](images/image_thumb_25255B64_25255D1.png)](http://lh4.ggpht.com/-XQuh6L1L0tw/UifgugLO1wI/AAAAAAAAP_c/1JYVDLOPvWQ/s1600-h/image%25255B180%25255D.png)

Next we push this branch into **_TeamMentor/Dev_**

[![image](images/image_thumb_25255B65_25255D1.png)](http://lh6.ggpht.com/-IDKkoNuEXZE/Uifgv5JzYpI/AAAAAAAAP_s/x7uYeae7kW8/s1600-h/image%25255B183%25255D.png)

At this moment, in the GitHub repo, **TeamMentor/Dev**'s master and 3.5_Release point to the same commit (**16354b3ec1757f56f0ee1594de3c72bb506f6537**):

[![image](images/image_thumb_25255B67_25255D1.png)](http://lh3.ggpht.com/-OWeof-DtYR4/UifgySQyP4I/AAAAAAAAP_4/jqm8a1vmdGg/s1600-h/image%25255B189%25255D.png)

Now comes the sledgehammer :)

We're going to (first locally) do a hard reset into the **b97a470ffa173d67a9c74373593eea03eb7a2da4 **commit, using the command **$ git reset --hard b97a470ffa173d67a9c74373593eea03eb7a2da4 **(remember that this commit is the common one between _TeamMentor/Master _and_ TeamMentor/Dev_)

[![image](images/image_thumb_25255B68_25255D1.png)](http://lh6.ggpht.com/-ShHzfhmQNzE/Uifgzvd0PpI/AAAAAAAAQAI/CqpTaCtuulc/s1600-h/image%25255B192%25255D.png)

After this hard reset, the **_TeamMentor/Dev_** master is aligned with the 3.3.3_Release branch and v3.3.3 tag (previously created)

[![image](images/image_thumb_25255B69_25255D1.png)](http://lh5.ggpht.com/-9HW7Dxflb7I/Uifg0--SLDI/AAAAAAAAQAY/x_Q70DYZYeI/s1600-h/image%25255B195%25255D.png)

We can also double check this, by using the command **_$ git gui_**  
**_  
_**[![image](images/image_thumb_25255B71_25255D.png)](http://lh4.ggpht.com/-B7YsjobMUgo/Uifg142tOYI/AAAAAAAAQAo/BRhE3X5CD7k/s1600-h/image%25255B201%25255D.png)

... followed by the **_Visualize all Branch History_** menu option:

[![image](images/image_thumb_25255B80_25255D.png)](http://lh6.ggpht.com/-STklktLg0Qs/Uifg3I6yHiI/AAAAAAAAQA4/o04FshAruk0/s1600-h/image%25255B205%25255D.png)

...and see that the Issue_142 branch is now a child of the current **_TeamMentor/Dev_** master (which is in sync with the TeamMentor/Master master)

[![image](images/image_thumb_25255B70_25255D1.png)](http://lh4.ggpht.com/-gmCT2sbEr7g/Uifg4Xw3vTI/AAAAAAAAQBI/BICeyNROuQQ/s1600-h/image%25255B198%25255D.png)

Finally we are ready to apply the sledgehammer to the repository hosted at GitHub, by forcing a push using the command **_$ git push --f dev master:master_**  
**_  
_**[![image](images/image_thumb_25255B81_25255D.png)](http://lh6.ggpht.com/-J-eoUmXI8bo/Uifg5kfUV3I/AAAAAAAAQBU/1hdMPQEuPng/s1600-h/image%25255B208%25255D.png)

Which makes the TeamMentor/Master look like this:

[![image](images/image_thumb_25255B83_25255D.png)](http://lh4.ggpht.com/-5IHJJCpHKUE/Uifg6mUebfI/AAAAAAAAQBo/C-HUB57HAJU/s1600-h/image%25255B214%25255D.png)

... with the **Issue_142 **branch** **having the master/3.3.3_Release branch as parent (see rouge/brown line)

[![image](images/image_thumb_25255B84_25255D.png)](http://lh4.ggpht.com/-Y9bak5lulOg/Uifg78At_5I/AAAAAAAAQB4/-5EgIGDgQm8/s1600-h/image%25255B217%25255D.png)

... and the 3.5_Release branch containing the commits that ware previously in the master branch (see yellow line)

[![image](images/image_thumb_25255B85_25255D.png)](http://lh5.ggpht.com/-8TdQk-7KhHU/Uifg9JNFXII/AAAAAAAAQCI/KD3_3GFAGJw/s1600-h/image%25255B220%25255D.png)

Finally a look at the current branches in **_TeamMentor/Dev_** shows that the **Issue_142 **is correctly 1x commit ahead and 0x behind the master branch (which means that it is ready for a pull request)

  
[![image](images/image_thumb_25255B87_25255D.png)](http://lh4.ggpht.com/-4sMiOBKulo0/UifgTYzDlGI/AAAAAAAAP98/8lBIDjuCNZY/s1600-h/image%25255B226%25255D.png)

**Appendix 5) Creating a 3.4_Release Feature branch and merging branches**  
**  
**At this point we have these branches ready to commit (via a pull request)

[![image](images/image_thumb_25255B93_25255D.png)](http://lh5.ggpht.com/-mnPuD506m1s/Uifg-T1oCPI/AAAAAAAAQCY/IZsmrPfmU4I/s1600-h/image%25255B244%25255D.png)

Instead of merging them into the **_TeamMentor/Dev _**master branch, we are going to create a **_TeamMentor/Dev _****_3.4_Release_** branch using the command **_$ git checkout -b 3.4_Release_** and push it to TeamMentor/Dev using the command **_$ git push dev 3.4_Release:3.4_Release_**  
**_  
_**[![image](images/image_thumb_25255B94_25255D.png)](http://lh4.ggpht.com/-Bg8Qt6KXn-U/Uifg_ql2JCI/AAAAAAAAQCo/jCBxfUcDt54/s1600-h/image%25255B247%25255D.png)

The reason for this branch is so that **_TeamMentor/Dev _**master branch is aligned with **_TeamMentor/Master_** master branch (which is the current official release), and only QA'd changes are pushed into **TeamMentor/Master **(first into 3.4_Release branch, and eventually into the official **_TeamMentor/Master _**master branch (note that we will most likely rename the **_TeamMentor/Master_** repo into **_TeamMentor/Release_**)

Next step is to create a pull request from the current Issue_XYZ branches into the 3.4_Release branch.

Let's start with **Issue_459,** by clicking on its Compare button:

[![image](images/image_thumb_25255B95_25255D1.png)](http://lh5.ggpht.com/-ec6vzm-ptmQ/UifhAjvbKzI/AAAAAAAAQC4/fMdRreUFS7k/s1600-h/image%25255B250%25255D.png)

On the next page, click on Edit:

[![image](images/image_thumb_25255B96_25255D1.png)](http://lh5.ggpht.com/-pgCvSLP0Cyc/UifhB7qG_lI/AAAAAAAAQDM/6fbuJdNCGb4/s1600-h/image%25255B253%25255D.png)

... to change the base branch (into 3.4_Release):

[![image](images/image_thumb_25255B98_25255D1.png)](http://lh5.ggpht.com/-k6R8T1d9bZw/UifhDFldc-I/AAAAAAAAQDc/7eWuJ2wdN2s/s1600-h/image%25255B259%25255D.png)

Then click on the **_Click to create a pull request for this comparison _**link

[![image](images/image_thumb_25255B99_25255D1.png)](http://lh3.ggpht.com/-nXb1LEZggo0/UifhEno5TBI/AAAAAAAAQDs/TdfTelNc8LI/s1600-h/image%25255B262%25255D.png)

... click on the _Send the Pull Request _button:

[![image](images/image_thumb_25255B100_25255D1.png)](http://lh6.ggpht.com/-WrhQyBuiXCU/UifhFsBkGwI/AAAAAAAAQD8/hfim6UoBgiY/s1600-h/image%25255B265%25255D.png)

... click on the **Merge pull request **button  
**_  
_**[![image](images/image_thumb_25255B101_25255D1.png)](http://lh4.ggpht.com/-m6NzkcDjxYg/UifhHcMH2sI/AAAAAAAAQEM/GymeqSun3lo/s1600-h/image%25255B268%25255D.png)

... and the _Confirm Merge _button:  
[![image](images/image_thumb_25255B102_25255D1.png)](http://lh3.ggpht.com/-3NfiDyNGrEU/UifhIjd9t3I/AAAAAAAAQEc/4k2MUW-cveE/s1600-h/image%25255B271%25255D.png)

We could now delete the branch (but I'm not going to do that at this stage, since first I want to see these merged branches in a GitHub Network Graph):

[![image](images/image_thumb_25255B103_25255D1.png)](http://lh4.ggpht.com/-iF6TJGlRlxY/UifhJ59lW0I/AAAAAAAAQEs/23a2opehJ4E/s1600-h/image%25255B274%25255D.png)

Back into the **_Branches not merged into master_** list, although the **_Issue_459_** branch is still 1x ahead of master, we now have the _**3.4_Release** _branch with 2x commits ahead:

[![image](images/image_thumb_25255B104_25255D1.png)](http://lh6.ggpht.com/-BQW6n_4rDmI/UifhLLj-VYI/AAAAAAAAQE8/7e37bKUrsHI/s1600-h/image%25255B277%25255D.png)

The two commits of the _**3.4_Release** _branch are one from the **_Issue_459_** branch and one from the pull request merge (note above how we could now do a Pull request from this **_3.4_Release_** branch into the **_master_** branch):

[![image](images/image_thumb_25255B105_25255D.png)](http://lh5.ggpht.com/-PNkQjeMcZjs/UifhMG-JZ3I/AAAAAAAAQFM/2pXw9zdW3G8/s1600-h/image%25255B280%25255D.png)

After doing the same workflow for **_Issue_475_** branch:

[![image](images/image_thumb_25255B106_25255D.png)](http://lh5.ggpht.com/-fwMagMQ89Lw/UifhNRCk_iI/AAAAAAAAQFc/RdFiFz4q1r0/s1600-h/image%25255B283%25255D.png)

... the **_3_4_Release_** branch is 4 commits ahead:

[![image](images/image_thumb_25255B107_25255D.png)](http://lh6.ggpht.com/-fgOVSW6NYow/UifhOwOzMnI/AAAAAAAAQFs/MJp6PJq08mY/s1600-h/image%25255B286%25255D.png)

And after doing the same workflow for the **_Issue_142, Issue_51_** and **Issue_400 **branches/issues_, _the **_3_4_Release _**is 10 commits ahead (with 5 Issues_Xyz applied):

[![image](images/image_thumb_25255B108_25255D.png)](http://lh3.ggpht.com/--clfyaWCj_8/UiffboXVkgI/AAAAAAAAPzs/6nNF8yIe8As/s1600-h/image%25255B289%25255D.png)

The TeamMentor/Dev graph also shows this workflow in action (note that If I had deleted branches after the pull request, we wouldn't see the tags in this network graph)

[![image](images/image_thumb_25255B109_25255D.png)](http://lh3.ggpht.com/-Cx5Ca-5vHAk/UiffeGE_hzI/AAAAAAAAP0M/TtUxVfEG95E/s1600-h/image%25255B292%25255D.png)

One important note is that the **_Issue_384_** didn't merge automatically with the 3.4_Release, which means that there is a conflict between one of the changes made by the applied branches and this code (i.e. Michael will need to fix this and resubmit the patch)

[![image](images/image_thumb_25255B110_25255D.png)](http://lh5.ggpht.com/-oLuU4zsjaI4/UifhP3yywCI/AAAAAAAAQF8/PPND-qUKesk/s1600-h/image%25255B295%25255D.png)

**  
****Wrapping up: Feedback and better git commands:**

If you made it this far to the end, it would be great to have some feedback on this git workflow (and solution).

And if you know of better ways to do solve probs like this one, please ping us with your ideas, since there is still far too much Git functionality that I/we are not aware of.

  

