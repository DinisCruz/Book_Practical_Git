## Changing the 'View TM article by anonymous users' status via GitHub 

From the 3.3. release of TeamMentor (TM) it is now possible to change configuration settings of live servers directly from GitHub.

For example I just published a QA version of the [https://services.teammentor.net](https://services.teammentor.net/) site on Azure's [https://tm-services.azurewebsites.net](https://tm-services.azurewebsites.net/)

Here is what [https://services.teammentor.net](https://services.teammentor.net/)  (on version 3.2.3) looks like:

[![image](images/image_thumb1.png)](http://lh5.ggpht.com/-vie5FTlgcIk/UVCsTrqahGI/AAAAAAAALNM/-70Vt9tTTJQ/s1600-h/image%25255B2%25255D.png)

Here is what [https://tm-services.azurewebsites.net](https://tm-services.azurewebsites.net/) (on version 3.3 RC4) looks like:

[![image](images/image_thumb_25255B1_25255D1.png)](http://lh5.ggpht.com/-JjPTE4ofhSw/UVCsVf0_lnI/AAAAAAAALNY/hoArqcwGH50/s1600-h/image%25255B5%25255D.png)

Can you spot the difference?

Here is the file (on GitHub) that controls if Anonymous users should be able to see TM's articles:

[![image](images/image_thumb_25255B2_25255D1.png)](http://lh6.ggpht.com/-2Ps7RbBZPqM/UVCsXG-JDlI/AAAAAAAALNo/EdVb3Lw_WZI/s1600-h/image%25255B8%25255D.png)

So the solution is to edit this file (in GitHub):

[![image](images/image_thumb_25255B3_25255D1.png)](http://lh3.ggpht.com/-5hUAiIfSACw/UVCsY1oraOI/AAAAAAAALN4/GZLkA0a9Ikg/s1600-h/image%25255B11%25255D.png)

change that value to true:

[![image](images/image_thumb_25255B4_25255D1.png)](http://lh4.ggpht.com/-S-ffzj9ODO0/UVCsaVdCbMI/AAAAAAAALOI/3mk00KK-dMI/s1600-h/image%25255B14%25255D.png)

Commit that change in GitHub's UI:

[![image](images/image_thumb_25255B5_25255D1.png)](http://lh6.ggpht.com/-9YJJ-DFmWfQ/UVCsb1yKnuI/AAAAAAAALOY/-hAvzVwQqIk/s1600-h/image%25255B17%25255D.png)

With this commit being now part of this repository:

[![image](images/image_thumb_25255B6_25255D1.png)](http://lh3.ggpht.com/-XdijUnzcEHA/UVCsdRJVZFI/AAAAAAAALOo/3VmJnWp4eZA/s1600-h/image%25255B20%25255D.png)

Next we go into the new Tbot interface ([https://tm-services.azurewebsites.net/tbot](https://tm-services.azurewebsites.net/tbot) ), which requires admin privs:

[![image](images/image_thumb_25255B7_25255D1.png)](http://lh5.ggpht.com/-xZx_UUHcVtU/UVCseorW6pI/AAAAAAAALO4/VJMpYF054UY/s1600-h/image%25255B23%25255D.png)

After login , open the **_'Reload Server Objects'_** page

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh4.ggpht.com/-gH3Hwaou6cs/UVCsgAXLCFI/AAAAAAAALPM/JIQSnf4NK3c/s1600-h/image%25255B29%25255D.png)

And click on the **_Reload UserData (and Git Pull and Push) _**button

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh3.ggpht.com/-jamM9O6YrGA/UVCsh39f_5I/AAAAAAAALPY/IRC7vi3e7Qs/s1600-h/image%25255B32%25255D.png)

which when executed:

[![image](images/image_thumb_25255B11_25255D1.png)](http://lh3.ggpht.com/-OJHBvjnTHjo/UVCsjJQGfaI/AAAAAAAALPs/RJYE0WGIym8/s1600-h/image%25255B35%25255D.png)

will have updated the local TMConfig.config file:

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh4.ggpht.com/-T0NhZJg8nbA/UVCskw3ARnI/AAAAAAAALP4/dP06qahsn5U/s1600-h/image%25255B38%25255D.png)

And if we logout, we will see the expected behavior:

[![image](images/image_thumb_25255B13_25255D1.png)](http://lh4.ggpht.com/-vCmowuMwJ9g/UVCsmc2GCLI/AAAAAAAALQI/_MNxqaOF92w/s1600-h/image%25255B41%25255D.png)

Finally, if we look at GitHub's commit history, we will see the commit we did in GitHub nicely merged with the commits that happened at the live server

[![image](images/image_thumb_25255B14_25255D1.png)](http://lh5.ggpht.com/-kWSKHdG13P4/UVCsn3QNs8I/AAAAAAAALQY/IeERG9F8slw/s1600-h/image%25255B44%25255D.png)

Here is the GitHub's Network Graph of this repositry, which shows both types of commits (the ones performed at at the live server vs the one at GitHub)

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh4.ggpht.com/-0-bTMupNw1c/UVCspDub51I/AAAAAAAALQo/hoJI3dp8LgI/s1600-h/image%25255B47%25255D.png)
