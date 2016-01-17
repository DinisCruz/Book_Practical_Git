## Using NGit to create native Git support in Azure deployed app (with automatic pushes and pulls)

This entry will show a pretty powerful new feature in [TeamMentor](http://teammentor.net/) (TM) which I'm very proud and excited about!

This feature is so important, that it literary caused a delay on the release of TM 3.3 for about 1 month (my instinct was pushing me on this direction since I 'knew' that this could be done, and that it would be a killer feature). Btw, there is a lot more NGit/Git support than what is shown here, but I'm sure you will see the power in the workflow described below.

Basically, TM's backend engine will now automatically perform:

  * a _**git pull  **-** **_when the TM server starts (or it cache is rebuilt) 
  * a **_git commit_** followed by a _**git push **- _on every library edit (on both content and structure changes).

  


And since TM uses the .NET Library [NGit](http://blog.diniscruz.com/search/label/NGit), what we have here is a pretty powerful **self-contained .Net-based** **'_git for content versioning'_** solution.

Practically speaking, **this is a Git workflow that runs on Azure-hosted-site without requiring Git to be installed on the live servers! **

This solves the problem created by the lack of git.exe (and supporting files) on an Azure's deployed web application (Azure's git support is limited to pushing code to Azure's servers, which will trigger  MSBuild-like website publishing workflow)

**Here is a example of this managed Git workflow in action.**  
**  
**The [https://tm-tm4tm.azurewebsites.net](https://tm-tm4tm.azurewebsites.net/) site:

[![image](images/image_thumb_25255B2_25255D1.png)](http://lh3.ggpht.com/-R7va5uLkp3o/UVZJy3tBFPI/AAAAAAAAAp4/QKP8I7XfTJY/s1600-h/image%25255B8%25255D.png)

is currently configured to use the UserData from this repository

[![image](images/image_thumb_25255B3_25255D1.png)](http://lh4.ggpht.com/-hD8mn4Doqck/UVZJ0Z9os_I/AAAAAAAAAqI/PQ0BdUj-AEE/s1600-h/image%25255B11%25255D.png)

which contains a reference to the [https://github.com/TMContent/Lib_TM4TM](https://github.com/TMContent/Lib_TM4TM) repository:

[![image](images/image_thumb_25255B4_25255D1.png)](http://lh6.ggpht.com/-IsKfPsttqq4/UVZJ1V8GROI/AAAAAAAAAqY/-cLt7a4_BD4/s1600-h/image%25255B14%25255D.png)

In practice, what this means is that the TM articles we see in [https://tm-tm4tm.azurewebsites.net](https://tm-tm4tm.azurewebsites.net/) are the ones hosted and managed  by the [https://github.com/TMContent/Lib_TM4TM](https://github.com/TMContent/Lib_TM4TM) repository.

But since the mapping is done via NGit and the account used (in Azure) to connect to GitHub's Lib_TM4TM has push privileges, it is now possible to make a change in [https://tm-tm4tm.azurewebsites.net](https://tm-tm4tm.azurewebsites.net/) that is auto committed locally and then into [https://github.com/TMContent/Lib_TM4TM](https://github.com/TMContent/Lib_TM4TM)

****  
**Auto Committing and pushing changes**  
**  
**For example, here are the last commits at [https://github.com/TMContent/Lib_TM4TM](https://github.com/TMContent/Lib_TM4TM)

[![image](images/image_thumb_25255B5_25255D1.png)](http://lh4.ggpht.com/-JYSHHDRuXXY/UVZJ2a-cyaI/AAAAAAAAAqo/qjAE-oxXyt4/s1600-h/image%25255B17%25255D.png)

In the [https://tm-tm4tm.azurewebsites.net](https://tm-tm4tm.azurewebsites.net/) server, lets' add an new Guidance Item (i.e. an Article)

[![image](images/image_thumb_25255B6_25255D1.png)](http://lh3.ggpht.com/-ui1TIvHDvEM/UVZJ3gLy1UI/AAAAAAAAAq4/aQpfSlaYm9s/s1600-h/image%25255B20%25255D.png)

Since (in TM 3.3) the articles are created immediately, by the time the editor is shown, the article shown in the popup-window will already exist on disks (i.e. there is already an **_384ed731-96a1-4c00-a830-345abfc827e2.xml_** file on the server)

[![image](images/image_thumb_25255B7_25255D1.png)](http://lh3.ggpht.com/-3aIrqrthutw/UVZJ46h16yI/AAAAAAAAArI/bFnDE-2rmP4/s1600-h/image%25255B23%25255D.png)

And with the new **'auto Git commit'** feature, the git commit of the new article will be available (after a couple secs) at GitHub:

[![image](images/image_thumb_25255B8_25255D1.png)](http://lh4.ggpht.com/-pG8F-6Fx0Zw/UVZJ59kGDcI/AAAAAAAAArY/wmntGzjab2w/s1600-h/image%25255B26%25255D.png)

This **_'commit on new article_**' is made of two file changes:  


  * The new article (the **_384ed731-96a1-4c00-a830-345abfc827e2.xml_** file)
  * The mapping of the new Article's GUID to the chosen 'view' element (which is part of the**_ Tm4TM.xml _**library xml file)

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh4.ggpht.com/-CC5BmAaNNeM/UVZJ63bSBOI/AAAAAAAAAro/b_1A5jyvWOw/s1600-h/image%25255B38%25255D.png)

**Next let's make some changes to the new article:**

[![image](images/image_thumb_25255B9_25255D1.png)](http://lh6.ggpht.com/-AGVe3KMBBFM/UVZJ8L6blpI/AAAAAAAAAr4/egDwCN368k0/s1600-h/image%25255B29%25255D.png)

After saving, the article is now available at

[https://tm-tm4tm.azurewebsites.net/article/384ed731-96a1-4c00-a830-345abfc827e2](https://tm-tm4tm.azurewebsites.net/article/384ed731-96a1-4c00-a830-345abfc827e2) or   
[https://tm-tm4tm.azurewebsites.net/article/Git_Support_for_Libraries](https://tm-tm4tm.azurewebsites.net/article/Git_Support_for_Libraries)

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh3.ggpht.com/-7V2lYmmqPkE/UVZJ9Q7H2hI/AAAAAAAAAsI/AWgk28DhrhI/s1600-h/image%25255B32%25255D.png)

As before, there is a new Commit at GitHub ([https://github.com/TMContent/Lib_TM4TM/commits/](https://github.com/TMContent/Lib_TM4TM/commits/)):

[![image](images/image_thumb_25255B14_25255D1.png)](http://lh5.ggpht.com/-5BLF2vX-E4M/UVZJ-tf0HkI/AAAAAAAAAsY/pnBzHUJbkBI/s1600-h/image%25255B44%25255D.png)

Which contains the 'metadata changes' and the new article's html content (created by the WYSIWYG TM online editor):

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh5.ggpht.com/-mE84h5FUkJE/UVZJ_oQ0W_I/AAAAAAAAAso/mIshjDFPhTY/s1600-h/image%25255B47%25255D.png)

And since this is all Git based, many more complex and multi-user/hosting scenarios are easily supported (for example I can have a local copy of the TM4TM server/repo which I can edit offline and push to GitHub (directly or via Pull Requests)).

The git merge strategy is the same used by GitHub:

  * If there are no conflicting changes, everything happens automatically or via GUIs pages
  * If there are merge conflicts, the Git Bash and Windows Diff tools should be used to address them
