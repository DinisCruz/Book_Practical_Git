## Changing the 'View TM article by anonymous users' status via GitHub

From the 3.3. release of TeamMentor (TM) it is now possible to change configuration settings of live servers directly from GitHub.

For example I just published a QA version of the [https://services.teammentor.net](https://services.teammentor.net/) site on Azure's [https://tm-services.azurewebsites.net](https://tm-services.azurewebsites.net/)

Here is what [https://services.teammentor.net](https://services.teammentor.net/)  (on version 3.2.3) looks like:

![](images/changing-view-1.png)

Here is what [https://tm-services.azurewebsites.net](https://tm-services.azurewebsites.net/) (on version 3.3 RC4) looks like:

![](images/changing-view-2.png)

Can you spot the difference?

Here is the file (on GitHub) that controls if Anonymous users should be able to see TM's articles:

![](images/changing-view-3.png)

So the solution is to edit this file (in GitHub):

![](images/changing-view-4.png)

change that value to true:

![](images/changing-view-5.png)

Commit that change in GitHub's UI:

![](images/changing-view-6.png)

With this commit being now part of this repository:

![](images/changing-view-7.png)

Next we go into the new Tbot interface ([https://tm-services.azurewebsites.net/tbot](https://tm-services.azurewebsites.net/tbot) ), which requires admin privs:

![](images/changing-view-8.png)

After login , open the **_'Reload Server Objects'_** page

![](images/changing-view-9.png)

And click on the **_Reload UserData (and Git Pull and Push)_** button

![](images/changing-view-10.png)

which when executed:

![](images/changing-view-11.png)

will have updated the local TMConfig.config file:

![](images/changing-view-12.png)

And if we logout, we will see the expected behavior:

![](images/changing-view-13.png)

Finally, if we look at GitHub's commit history, we will see the commit we did in GitHub nicely merged with the commits that happened at the live server

![](images/changing-view-14.png)

Here is the GitHub's Network Graph of this repository, which shows both types of commits (the ones performed at at the live server vs the one at GitHub)

![](images/changing-view-15.png)
