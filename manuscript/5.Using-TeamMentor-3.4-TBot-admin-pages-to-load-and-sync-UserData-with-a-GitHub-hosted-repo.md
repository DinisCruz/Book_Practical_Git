## Using TeamMentor 3.4 TBot admin pages to load and sync UserData with a GitHub hosted repo

Continuing from where [Using TeamMentor 3.4 TBot admin pages to load and sync a Library hosted on GitHub](http://blog.diniscruz.com/2014/01/using-teammentor-34-tbot-admin-pages-to.html) left, this post shows how to use the same technique to sync TeamMentor's UserData with a GitHub repo.

For more details on how the **_UserData_** _repo/folder_ fits within TeamMentor's architecture, see these posts:   
* [Writing RazorSharp script to import TeamMentor users](http://blog.diniscruz.com/2013/03/writing-razorsharp-script-to-import.html)
* [Creating QA versions of TeamMentor UserData repository, and using branches to show/test the multiple config options](http://blog.diniscruz.com/2013/04/creating-qa-versions-of-teammentor.html)
* [Creating a version TeamMentor which uses the new GitUserData.config file](http://blog.diniscruz.com/2013/03/creating-version-teammentor-which-uses.html)
* [Practical Example of using Web CSharpREPL in TeamMentor's development/customizations](http://blog.diniscruz.com/2013/04/practical-example-of-using-web.html)
* [Using CSharpRepl to batch change TeamMentor's users email and settings](http://blog.diniscruz.com/2013/04/using-csharprepl-to-batch-change.html)
* [Running Customized C# code loaded from TeamMentor's UserData repository](http://blog.diniscruz.com/2013/04/running-customized-c-code-loaded-from.html)
* [Using NGit to create native Git support in Azure deployed app (with automatic pushes and pulls)](http://blog.diniscruz.com/2013/03/using-ngit-to-create-native-git-support.html)

**Step 1: Create UserData repo in GitHub**

The first task is to create a **Private** repo to hold the _UserData_ contents.

Important: Because it will contain sensitive data about the target TeamMentor instance (like password hashes, session IDs, emails, user activity tracking, SMTP account details and encryption key/salt), don't create a Public repo!

In GitHub, login into the desired account and go to the **_New Repository_** page:

![](images/Screen_Shot_2014-01-29_at_13_17_41.png)

In this case I'm going to create the **_Site_TM_34_QA_Azure_** repo, where I followed a convention that we have for UserData repos nanes: _Site_{Url} _or _Site_{ServerType}_. Which in this case is **Site_TM_34_QA_Azure**

![](images/Screen_Shot_2014-01-29_at_13_18_02.png)

**Step 2: Make sure the repo is created with at least one file**  

If you chose the option to add a default README file in the previous step, you can ignore this, but if you didn't you will need to make sure that this repo has at least one branch and one file (or the Git Clone from TeamMentor will be left in a non-working state).

The good news is that you can easily do that from GitHub's interface.

On the **_Quick_** **_setup_** section, click on the **_README_** me link:

![](images/Screen_Shot_2014-01-29_at_13_34_20.png)

... which will open a web UI where the README.md file can be created:

![](images/Screen_Shot_2014-01-29_at_13_34_01.png)

And after clicking on **_Commit New File_**

![](images/Screen_Shot_2014-01-29_at_13_34_08.png)

... the target repo is now in state that can be used by TeamMentor

![](images/Screen_Shot_2014-01-29_at_13_33_51.png)

**Step 3: Create a GitHub Personal Access Token to be used to access this account from TM server**  

As with the [previous scenario](http://blog.diniscruz.com/2014/01/using-teammentor-34-tbot-admin-pages-to.html), that is done on this Admin page

![](images/Screen_Shot_2014-01-29_at_13_19_49.png)

On the resulting page, copy the token (in this case c78fa4d5dcf1b9f521a99396d667a00297734a2b )

![](images/Screen_Shot_2014-01-29_at_13_19_58.png)

This Token will used together with the HTTPS git url ([https://github.com/DinisCruz-Dev/Site_TM_34_QA_Azure.git](https://github.com/DinisCruz-Dev/Site_TM_34_QA_Azure.git)) in the format: http://**{username}**:**{password/token}**@github.com/**{GitUser}**/**{TargetRepo}**.git.  In this case:

https://DinisCruz-Dev:c78fa4d5dcf1b9f521a99396d667a00297734a2b@github.com/DinisCruz-Dev/Site_TM_34_QA_Azure.git

  **Step 4: Configure TeamMentor Server to use GitHub's UserData repo:**

next open TBot's _Edit GitUserLocation_ page:

![](images/Screen_Shot_2014-01-29_at_13_21_02.png)

... and enter the Git Url (shown above) in the **_Git User Location_** textbox:

![](images/Screen_Shot_2014-01-29_at_13_21_18.png)

Important: In order to keep the UserData up-to-date, it is also needed to set the _TmConfig.config_'s _AutoCommit_UserData_ value to **_true_**

![](images/Screen_Shot_2014-01-29_at_13_24_13.png)

Once that is done, reload the server cache (which will trigger the UserData setup):

![](images/Screen_Shot_2014-01-29_at_13_22_59.png)

Once that is completed, you will notice that you are logged out from TM.

![](images/Screen_Shot_2014-01-29_at_13_24_54.png)

This happened because a new **_UserData_** user store was created which didn't not had any accounts. In those cases TeamMentor server engine will create a default admin account using the details provided in **_TMConfig.config:_**

![](images/Screen_Shot_2014-01-29_at_13_25_09.png)

We can also double check on the _TBot's_ _DebugInfo_ page that the UserData now points to a different folder (note that the folder name is based on the repo name)

![](images/Screen_Shot_2014-01-29_at_13_26_48.png)

We can also confirm in the **DinisCruz-Dev/Site_TM_34_QA_Azure** repo that the UserData default files have been created (which also confirms that the connection between TeamMentor and Git's UserData repo is working ok)

![](images/Screen_Shot_2014-01-29_at_13_41_16.png)

**Step 5: Create a new user and confirm that it shows up in GitHub**  

If you look at the Users folder in the GitHub repo, you should see on file in there (which represents the default admin user)

![](images/Screen_Shot_2014-01-29_at_13_41_27.png)

Next, create a new user (using for example the form provided in the home page of the target TeamMentor site):

![](images/Screen_Shot_2014-01-29_at_13_42_20.png)

Once the account is created:

![](images/Screen_Shot_2014-01-29_at_13_42_26.png)

Go back to TBot and reload the UserData (which will trigger a Git Pull and Push of the UserData repo):

![](images/Screen_Shot_2014-01-29_at_13_42_34.png)

Reload the GitHub User's folder and notice that there are two xml files in there:

![](images/Screen_Shot_2014-01-29_at_13_42_41.png)

A quick look at the commits of this repo, will also show the Commits created by TeamMentor's backend:

![](images/Screen_Shot_2014-01-29_at_13_43_14.png)

Now logout the admin user and login as the new **_dinis_** user:

![](images/Screen_Shot_2014-01-29_at_13_54_45.png)

... reload the UserData objects:  

![](images/Screen_Shot_2014-01-29_at_13_54_59.png)

... and note in UserData GitHub's repo that there are a number of new commits:

![](images/Screen_Shot_2014-01-29_at_13_55_20.png)

For example, here is the 'Logout user activity log' for the admin user:

![](images/Screen_Shot_2014-01-29_at_13_55_33.png)

... and here is the UserActivity for the **_dinis_** user:  

![](images/Screen_Shot_2014-01-29_at_13_56_07.png)

**Step 6: Add a Library from a GitHub Repo**  

In order to make this a working server, we need to update the SecretData config file:

![](images/Screen_Shot_2014-01-29_at_13_45_50.png)

With the location of the Library GitHit repo (see [Using TeamMentor 3.4 TBot admin pages to load and sync a Library hosted on GitHub](http://blog.diniscruz.com/2014/01/using-teammentor-34-tbot-admin-pages-to.html) for a detailed explanation of its origin)

![](images/Screen_Shot_2014-01-29_at_13_46_04.png)

Next reload the Cache:

![](images/Screen_Shot_2014-01-29_at_13_51_42.png)

On completion you should see a message with the number of Libraries and Articles in the current server:

![](images/Screen_Shot_2014-01-29_at_13_52_45.png)

And reloading TeamMentor will show the imported Library fully loaded and ready to be used:

![](images/Screen_Shot_2014-01-29_at_13_54_10.png)
