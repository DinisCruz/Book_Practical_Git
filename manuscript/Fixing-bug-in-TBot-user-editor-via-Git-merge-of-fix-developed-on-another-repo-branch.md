## Fixing bug in TBot user editor via Git merge of fix developed on another repo's branch

Here is an example of how I just created a HotFix branch to address an issue we want to push to our live servers asap, and how the fix was developed by Ian in one of this dev branches.

First I created _HotFix _Branch at a (freshly baked) local clone of the **_TeamMentor/Dev_** repository:  

![](images/fixing-bug-tbot-1.png)

Then I reviewed the code from Ian's branch I want to merge:

![](images/fixing-bug-tbot-2.png)

When happy with the changes, I used a **_git fetch** to get the latest version of Ian's fork of **_TeamMentor/Dev_**

![](images/fixing-bug-tbot-3.png)

![](images/fixing-bug-tbot-4.png)

Followed by a **_$ git merge Dev_Ian/#437-Password-Expiry HotFix_3_3_1_**  

![](images/fixing-bug-tbot-5.png)

Which did the merge with the**_ TeamMentor/Dev_** master branch

A look at GitK confirms that there was only one commit added (the Ian's '[Date value being saved to database](https://github.com/IanIan123/Dev/commit/32bd09708bc60c7e3d7e5e0c6d74a1f3c19c5915)')

![](images/fixing-bug-tbot-6.png)

At this stage if we look at Ian's network map, we will see that this commit is not linked to another commit (i.e. is the last one of the **_#437-Password-Expiry_** branch

![](images/fixing-bug-tbot-7.png)

Next step is to quickly test if the feature is working ok.

This fix is for the [Password expiry cannot be set from the main TM GUI](https://github.com/TeamMentor/Master/issues/437) issue  (i.e. make the 'Account Expiration' field editable).

So I opened an user's edit page

![](images/fixing-bug-tbot-8.png)

changed the expiration date:

![](images/fixing-bug-tbot-9.png)

Saved it

![](images/fixing-bug-tbot-9a.png)

And confirmed that the user's xml data was changed on the in-memory version of the user xml files:

![](images/fixing-bug-tbot-10.png)

and on the file system:

![](images/fixing-bug-tbot-11.png)

My final step was to push the HotFix branch into the live server:

![](images/fixing-bug-tbot-12.png)

Here are the commits in the new **_HotFix_3_3_1_** branch (note the Ian's '[Date value being saved to database](https://github.com/IanIan123/Dev/commit/32bd09708bc60c7e3d7e5e0c6d74a1f3c19c5915)' branch is now there)

![](images/fixing-bug-tbot-13.png)

And now Ian's branch is connected with the new HotFix_3_3_1 branch:

![](images/fixing-bug-tbot-14.png)

same graph without the branch labels:

![](images/fixing-bug-tbot-15.png)
