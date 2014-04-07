##  Using Git Branches to fix Issues added to TeamMentor's GitHub repository 

This is the currently workflow that I'm following when coding/fixing TeamMentor Issues added to the [TeamMentor/Master/Issues](https://github.com/TeamMentor/Master/issues) list.  


  * Find issue to address
  * Create and checkout new branch (with the issue ID on its title)
  * Apply the fixes (on the new branch)
  * Commit the changes (on the new branch)
  * Checkout master branch
  * Merge changes (from new branch) into master , using the --no--ff (no fast-forward) option (this is very important, see [here](http://stackoverflow.com/questions/6701292/git-fast-forward-vs-no-fast-forward-merge) and [here](http://stackoverflow.com/questions/2850369/why-does-git-use-fast-forward-merging-by-default/2850413#2850413) for a good explanation why)
  * Push to GitHub

**Lets look at this in action.**  

Here is a simple issue to fix: [https://github.com/TeamMentor/Master/issues/389](https://github.com/TeamMentor/Master/issues/389)

[![image](images/image_thumb_25255B1_25255D1.png)](http://lh4.ggpht.com/-9dFF2Pi1Uik/UVXNUil8GkI/AAAAAAAAAe4/nZaS3DpXfvU/s1600-h/image%25255B5%25255D.png)

In GitHub, the issue is #389 , so on a local clone of the Master repository, we create a branch called**_ Issue_389 _**(using the --b switch to create it)

[![image](images/image_thumb_25255B2_25255D1.png)](http://lh3.ggpht.com/-NL-Cp-JN4uQ/UVXNWPLtl8I/AAAAAAAAAfI/c-rWtY8mF8g/s1600-h/image%25255B8%25255D.png)

In VisualStudio, apply the fix to the code:

[![image](images/image_thumb_25255B3_25255D1.png)](http://lh4.ggpht.com/-QVG4VglEIp0/UVXNXCLqt3I/AAAAAAAAAfY/QI_OeblrcMs/s1600-h/image%25255B11%25255D.png)

Quickly look in a browser to confirm the change (this should also be reconfirmed via a UI UnitTest):

[![image](images/image_thumb_25255B7_25255D1.png)](http://lh3.ggpht.com/-XH1-lE75Yho/UVXNYt3bkbI/AAAAAAAAAfo/lYH5bjXgHEw/s1600-h/image%25255B17%25255D.png)

Commit the change to the **Issue_389 **branch:

[![image](images/image_thumb_25255B8_25255D1.png)](http://lh3.ggpht.com/-yeAXjaQsR20/UVXNZ4TuevI/AAAAAAAAAf4/UPB4D8aergY/s1600-h/image%25255B20%25255D.png)

Which means that at this moment, there is nothing else to commit on the **_Issue_389 _**branch:

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh5.ggpht.com/-5dCVFqlwHs8/UVXNbUWCUtI/AAAAAAAAAgI/zuTbsAJ7SV4/s1600-h/image%25255B23%25255D.png)

which is now one commit ahead of master

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh3.ggpht.com/-TcFJSVI15Fk/UVXNcphnWkI/AAAAAAAAAgY/0roSZEQYzEI/s1600-h/image%25255B26%25255D.png)

Next step is to **_checkout _**(into) master and do the **_git merge_** using the **_--no--ff _**

[![image](images/image_thumb_25255B11_25255D1.png)](http://lh5.ggpht.com/-rkx8vTRNFaU/UVXNd9qAeoI/AAAAAAAAAgo/Eq7SVZI-Das/s1600-h/image%25255B29%25255D.png)

Gitk shows the effect of the **_--no--ff_** (ie. the use of the branch was preserved)

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh6.ggpht.com/-mmM2n1a8W8s/UVXNfS5TMfI/AAAAAAAAAg4/0KCPwgNkcpo/s1600-h/image%25255B32%25255D.png)

Final step is to push the commits to GitHub:

[![image](images/image_thumb_25255B13_25255D1.png)](http://lh4.ggpht.com/-s_3qpErWWLU/UVXNhQohLCI/AAAAAAAAAhI/FQty1YFAXJs/s1600-h/image%25255B35%25255D.png)

Here is the commit at GitHub:

[![image](images/image_thumb_25255B14_25255D1.png)](http://lh3.ggpht.com/-hYlowFTS0Io/UVXNjG_VoGI/AAAAAAAAAhY/DfJu6ph6LsU/s1600-h/image%25255B38%25255D.png)

Here is the GitHub's Network view:

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh3.ggpht.com/-dEe01gH0zM0/UVXNkP4pbHI/AAAAAAAAAho/iH-mO_8goEo/s1600-h/image%25255B41%25255D.png)
