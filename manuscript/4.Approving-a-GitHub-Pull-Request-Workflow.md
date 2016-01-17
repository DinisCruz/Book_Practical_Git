## Approving a GitHub Pull Request Workflow

I just received a GitHub's **_Pull Request_** from Roman for some new content that he added to TeamMentor's Documentation Site.

Here is the workflow I used to approve this request using GitHub's web-based workflow:

**1) Receive GitHub email alert:**  

![](images/Screen_Shot_2012-10-17_at_01_46_01.png)

**2) Go to GitHub and see the Pull Request there:**

The main page ([https://github.com/TeamMentor/TeamMentor-Documentation/pull/4](https://github.com/TeamMentor/TeamMentor-Documentation/pull/4)) gives us a nice overview of the Pull Request:  

![](images/Screen_Shot_2012-10-17_at_01_48_15.png)

Here are the Commits:

![](images/Screen_Shot_2012-10-17_at_01_48_47.png)

On the **_Files Changed_** tab we can easily see (in colours) the proposed changes.

For example, here is a change to the main TM Library xml file with a couple new articles added:  

![](images/Screen_Shot_2012-10-17_at_01_48_58.png)

Here are a couple lines removed and some added:

![](images/Screen_Shot_2012-10-17_at_01_49_37.png)

This is a new file:

![](images/Screen_Shot_2012-10-17_at_01_50_03.png)

These are a couple metadata changes:

![](images/Screen_Shot_2012-10-17_at_01_50_13.png)

**3) Approving the Pull request**  

Going back to the first page (the **_Discussion_** tab) the most important part of this whole process is the green bar that shows that this Pull Request can be merged ok

![](images/Screen_Shot_2012-10-17_at_02_16_44.png)

This basically means that there are no conflicts between the new changes and the current content. When this is not possible (and you get a red bar), the best thing is to do this 'manually' (i.e. via a git bash on your local box)

When you click on the 'Merge Pull Request' button you get this confirmation request:

![](images/Screen_Shot_2012-10-17_at_02_20_16.png)

And clicking on 'Confirm Merge' will do the commit and close this Pull Request:

![](images/Screen_Shot_2012-10-17_at_02_21_28.png)
