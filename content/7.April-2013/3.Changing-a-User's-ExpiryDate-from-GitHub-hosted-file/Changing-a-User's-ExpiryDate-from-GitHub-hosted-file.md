## Changing a User's ExpiryDate from GitHub hosted file

For the cases where TeamMentor UserData is loaded from a GitHub repository, it is possible to change/manage user data directly from GitHub's web GUI (or from a local clone of that repository).

Lets take for example Danny's account, which is expired at the moment (today is 4/10/2013):

![](images/changing-users-1.png)

In GitHub, this is the file that contains Danny's user data:

![](images/changing-users-2.png)

So we open and edit that file:

![](images/changing-users-3.png)

Change the **_ExpirationDate_** to a value in 2014

![](images/changing-users-4.png)

Commit the changes:

![](images/changing-users-5.png)

Reload the UserData:

![](images/changing-users-6.png)

And the Danny account details at the server is now set to the new date:

![](images/changing-users-7.png)

This is one of the nice side effects of having the ability to push TM's user data into a Git repository (another advantage is that we now have fully backed-up, logged and hashed user's change-history)
