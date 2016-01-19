## Git pulling a TeamMentor Library and renaming it

Here is an example of how to use the new TM 3.3 capabilities to load libraries from GitHub and to rename them.

Let's start with a version of TM that looks like this:

![](images/saving-pulling-1.png)

And let's say that we wanted to add the TM4TM Library to this server

![](images/saving-pulling-2.png)

First thing to do is to copy the Git's **_Read-Only Url_**

![](images/saving-pulling-3.png)

And add it to the TBot's Secret Data file:

![](images/saving-pulling-4.png)

Before we reload the cache (which will do the git pull using NGit), lets see what the Library's folder looks like.

In this instance of TM, as we can see by the TMConfig.config file:

![](images/saving-pulling-5.png)

The Library files are located in the TM_Libraries_12 folder:

![](images/saving-pulling-6.png)

And if we now trigger the cache reload:

![](images/saving-pulling-7.png)

We will see that there is a new TM4TM folder:

![](images/saving-pulling-8.png)

which is a git repository

![](images/saving-pulling-9.png)

with its remote set to the Git;s **_Read-Only Url_**

![](images/saving-pulling-10.png)

After the cache reloads:

![](images/saving-pulling-11.png)

There are now 8 Libraries loaded in TM:

![](images/saving-pulling-12.png)

The reason for the extra 6 libraries (when we only added one new repository) is that from TM 3.3, there can be more than one library file in library folder (note: the recommendation is have one library xml file per folder)

![](images/saving-pulling-13.png)

Also note that the library name/caption is now independent from the xml file name:

![](images/saving-pulling-14.png)

Let's now open TM's Edit mode

![](images/saving-pulling-15.png)

and use it to rename the *TM4TM_RTST2* Library:  

![](images/saving-pulling-16.png)

from:

![](images/saving-pulling-17.png)

to:

![](images/image_thumb_25255B59_25255D.png)

After the rename, a number of thinks happened.

**1) The TM4TM.xml library file contents changed:**

![](images/saving-pulling-18.png)

**2) There was a local commit with the change:**

![](images/image_thumb_25255B61_25255D.png)

**3) the auto pull to GitHub failed**

This is confirmed by the commit list at GitHub:

![](images/image_thumb_25255B64_25255D.png)

and the 'push error' we got on the TBot's **_DebugInfo_** page

![](images/image_thumb_25255B62_25255D.png)

In this case I do want to push the changes, so back in GitHub I copied the **_SSH_** git url

![](images/image_thumb_25255B65_25255D.png)

And use it directly on a git push (I could also had done this by setting up a new remote)

![](images/image_thumb_25255B66_25255D.png)

Now the commit created by TM (on library rename) exists in GitHub:

![](images/image_thumb_25255B67_25255D.png)

**Removing the extra Library files:**

Since we don't need the extra libraries xml files, I just removed them (and committed the changes)

![](images/image_thumb_25255B68_25255D.png)

Which means that after cache reload,

![](images/image_thumb_25255B69_25255D.png)

there are now 3 libraries in my local TM instance:

![](images/image_thumb_25255B70_25255D.png)
