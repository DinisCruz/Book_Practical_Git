## Creating a clone of WebGoat on GitHub

I needed a couple vulnerable source code examples (to use on the new [TeamMentor](http://teammentor.net/) Eclipse plug-in) so an obvious option was to use [WebGoat](https://www.owasp.org/index.php/Category:OWASP_WebGoat_Project) (whose code is currently hosted at [Google Code page](https://code.google.com/p/webgoat/))

But since there wasn't a source code download option (in the current [download page](https://code.google.com/p/webgoat/downloads/list))

![](images/fork-webgoat-1.png)

... and this project is not using Git (sorry, but I can't use SVN anymore :) ... it's too painful)

![](images/fork-webgoat-2.png)

... I quickly created a clone of it using the **_$ git svn clone -s http://webgoat.googlecode.com/svn webgoat_**  

... which downloaded the entire source code and available history:

![](images/fork-webgoat-3.png)

When completed (it took a little bit since there was quite a bit of history)

![](images/fork-webgoat-4.png)

I had this **File Structure:**  

![](images/fork-webgoat-5.png)

and

![](images/fork-webgoat-6.png)

This Git repo **Size:**  

![](images/fork-webgoat-7.png)

This Git **History:**

![](images/fork-webgoat-8.png)

which goes back all the way to 2006!

![](images/fork-webgoat-9.png)

These **Braches:**

![](images/fork-webgoat-10.png)

Note that after the svn clone the current git **_master_** branch is the original svn **_truck._**  

But as we can see by the above list, there is already an **_webgoat-6.0_** branch going on (in fact most of the recent code updates are done there), so here is how we can create+checkout a git tracking branch for it:

![](images/fork-webgoat-11.png)

... which will make the file system look like this now:

![](images/fork-webgoat-12.png)

... and the Git History like this:

![](images/fork-webgoat-13.png)

Next step is to push this version to the newly created [https://github.com/OWASP/WebGoat](https://github.com/OWASP/WebGoat) repo (in OWASP GitHub organisation):

![](images/fork-webgoat-14.png)

On the local repo add a remote:

![](images/fork-webgoat-15.png)

... and **_push --all_**

![](images/fork-webgoat-16.png)

Once the upload completes:

![](images/fork-webgoat-17.png)

... the code will be at GitHub:

![](images/fork-webgoat-18.png)

including the **webgoat-6.0 branch:**  

![](images/fork-webgoat-19.png)

Finally I updated the OWASP WebGoat page to make references to this new GitHub repo:

![](images/fork-webgoat-20.png)

And that's it!

Now you can go to [https://github.com/OWASP/WebGoat](https://github.com/OWASP/WebGoat) and clone (or [download the zip](https://github.com/OWASP/WebGoat/archive/master.zip)) of OWASP's WebGoat :)
